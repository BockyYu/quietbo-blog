---
title: '[docker-compose] 服務的更新'
author: Bocky
type: post
date: 2022-02-01T18:11:04+00:00
url: /2022/02/02/docker-compose-服務的更新/
categories:
  - 'Docker&amp; Docker-compose'
tags:
  - docker-compose

---
## 服務更新 {#服務更新.wp-block-heading}

下方為目錄結構:

<pre class="wp-block-code"><code class="">$ tree      
.
├── docker-compose.yml
└── my_flask
    ├── app.py
    └── dockerfile</code></pre>

app.py檔如下

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">from flask import Flask
from redis import Redis
import os
import socket

app = Flask(__name__)
redis = Redis(host=os.environ.get('REDIS_HOST', '127.0.0.1'), port=6379)


@app.route('/')
def hello():
    redis.incr('hits')
    return f"Hello Container World! I have been seen {redis.get('hits').decode('utf-8')} times and my hostname is {socket.gethostname()}.\n"</code></pre>

dockerfile如下:

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">FROM python:3.9.5-slim

RUN pip install flask redis && \
    groupadd -r flask && useradd -r -g flask flask && \
    mkdir /src && \
    chown -R flask:flask /src

USER flask

COPY app.py /src/app.py

WORKDIR /src

ENV FLASK_APP=app.py REDIS_HOST=redis

EXPOSE 5000

CMD ["flask", "run", "-h", "0.0.0.0"]</code></pre>

docker-compose.yml檔內容如下:

<pre class="wp-block-code"><code lang="docker" class="language-docker line-numbers">version: "3.8"

services:
  flask-demo:
    build: ./my_flask
    image: flask_demo:latest
    environment:
      - REDIS_HOST=redis-server
    networks:
      - demo-network
    ports:
      - 8899:5000

  redis-server:
    container_name: redis-demo
    image: redis:latest
    networks:
      - demo-network

networks:
  demo-network: null</code></pre>

在該目錄下執行:

<pre class="wp-block-code"><code class="">docker-compose up -d</code></pre>

會創建2個容器，一個是flask-demo，一個是redis，開起瀏覽器輸入127.0.0.1:8899，會看到下方字串(隨著開啟次數會累加):

<pre class="wp-block-code"><code class="">Hello Container World! I have been seen 1 times and my hostname is b895a0c7b962.</code></pre>

若有更新app.py內的code，重新build一次flask，下方為演示的訊息:

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ docker-compose up -d --build
Building flask-demo
[+] Building 5.9s (10/10) FINISHED                                                                                                          
 =&gt; [internal] load build definition from Dockerfile                                                                                   0.0s
 =&gt; =&gt; transferring dockerfile: 37B                                                                                                    0.0s
 =&gt; [internal] load .dockerignore                                                                                                      0.0s
 =&gt; =&gt; transferring context: 2B                                                                                                        0.0s
 =&gt; [internal] load metadata for docker.io/library/python:3.9.5-slim                                                                   5.8s
 =&gt; [auth] library/python:pull token for registry-1.docker.io                                                                          0.0s
 =&gt; [internal] load build context                                                                                                      0.0s
 =&gt; =&gt; transferring context: 395B                                                                                                      0.0s
 =&gt; [1/4] FROM docker.io/library/python:3.9.5-slim@sha256:9828573e6a0b02b6d0ff0bae0716b027aa21cf8e59ac18a76724d216bab7ef04             0.0s
 =&gt; CACHED [2/4] RUN pip install flask redis &&     groupadd -r flask && useradd -r -g flask flask &&     mkdir /src &&     chown -R   0.0s
 =&gt; [3/4] COPY app.py /src/app.py                                                                                                      0.0s
 =&gt; [4/4] WORKDIR /src                                                                                                                 0.0s
 =&gt; exporting to image                                                                                                                 0.0s
 =&gt; =&gt; exporting layers                                                                                                                0.0s
 =&gt; =&gt; writing image sha256:cc1bafcde9c602150db215976497c20a13db386bdbfeecf41d84e36ed77286e9                                           0.0s
 =&gt; =&gt; naming to docker.io/library/flask_demo:latest                                                                                   0.0s

Use 'docker scan' to run Snyk tests against images to find vulnerabilities and learn how to fix them
redis-demo is up-to-date
Recreating mydocker_flask-demo_1 ... done</code></pre>

查看容器狀況，會發現原本的redis沒有被重構，只有因修改了app.py後重建的flask-demo，畫面如下:  
<img decoding="async" src="https://i.imgur.com/jTeoXcD.png" alt="" /> 

## 刪除服務 {#刪除服務.wp-block-heading}

將原本的docker-compose.yml檔新增一個busbox:

<pre class="wp-block-code"><code lang="docker" class="language-docker line-numbers">version: "3.8"

services:
  flask-demo:
    build: ./my_flask
    image: flask_demo:latest
    environment:
      - REDIS_HOST=redis-server
    networks:
      - demo-network
    ports:
      - 8899:5000

  redis-server:
    container_name: redis-demo
    image: redis:latest
    networks:
      - demo-network

  busybox:
    image: busybox:latest
    command: sh -c "while true; do sleep 3600; done"
    networks:
      - demo-network

networks:
  demo-network: null</code></pre>

在剛才已有兩個容器的狀況下，再下一次指令:

<pre class="wp-block-code"><code class="">docker-compose up -d</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/Z5Bn8Te.png" alt="" /> </figure> 

在已經建立3個容器的狀況下，將yml檔的busbox註解掉，再重新下一次指令，會出現一段WARNING的訊息:

<pre class="wp-block-code"><code class="">WARNING: Found orphan containers (mydocker_busybox_1) for this project. If you removed or renamed this service in your compose file, you can run this command with the --remove-orphans flag to clean it up.</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/Wf3b6zu.png" alt="" /> </figure> 

使用剛才建議的指令，來刪除不需要的service

<pre class="wp-block-code"><code class="">docker-compose up -d --remove-orphans</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/QsCEeSA.png" alt="" /> </figure> 

三個更新文件指令:

<pre class="wp-block-code"><code class=" line-numbers">docker-compose build # 只build dockerfile 的image
docker-compose up -d --remove-orphans # 刪除不需要使用的service
docker-compose restart # 重啟</code></pre>