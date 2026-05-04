---
title: '[Docker] Mac -Python Flask+Redis(練習)'
author: Bocky
type: post
date: 2022-01-21T19:48:54+00:00
url: /2022/01/22/docker-mac-python-flaskredis練習/
categories:
  - 'Docker&amp; Docker-compose'
tags:
  - docker

---
環境

<ul class="wp-block-list">
  <li>
    Mac M1
  </li>
  <li>
    docker:Version 20.10.11
  </li>
</ul>

<ol class="wp-block-list">
  <li>
    建立app.py
  </li>
</ol>

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

<ol class="wp-block-list" start="2">
  <li>
    同一層建立dockerfile
  </li>
</ol>

<pre class="wp-block-code"><code lang="docker" class="language-docker line-numbers">FROM python:3.9.5-slim

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

<ol class="wp-block-list" start="3">
  <li>
    image 的準備
  </li>
</ol>

<pre class="wp-block-code"><code class="">$ docker image pull redis
$ docker image build -t flask-demo .
$ docker image ls
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
flask-demo   latest    d92f7778af76   9 minutes ago   123MB
redis        latest    f16c30136ff3   4 weeks ago     107MB</code></pre>

<ol class="wp-block-list" start="4">
  <li>
    創建一個docker bridge
  </li>
</ol>

<pre class="wp-block-code"><code class="">$ docker network create -d bridge demo-network
960a617c97c6a197624c51fc02dbbf9007080662052551296d55b0cc7d5f2ba7
$ docker network ls
NETWORK ID     NAME           DRIVER    SCOPE
b2077f8151cb   bridge         bridge    local
caf0f586ef79   demo-network   bridge    local
d1465da885e1   host           host      local</code></pre>

<ol class="wp-block-list" start="5">
  <li>
    創建redis container<br />創建一個叫 redis-server 的container，連到demo-network上
  </li>
</ol>

<pre class="wp-block-code"><code class="">$ docker container run -d --name redis-server --network demo-network redis
960a617c97c6a197624c51fc02dbbf9007080662052551296d55b0cc7d5f2ba7

$ docker container ls
CONTAINER ID   IMAGE        COMMAND                  CREATED          STATUS          PORTS                    NAMES
960a617c97c6   redis        "docker-entrypoint.s…"   12 minutes ago   Up 12 minutes   6379/tcp                 redis-server</code></pre>

<ol class="wp-block-list" start="6">
  <li>
    創建flask container
  </li>
</ol>

<pre class="wp-block-code"><code class="">$ docker container run -d --network demo-network --name flask-demo --env REDIS_HOST=redis-server -p 5000:5000 flask-demo</code></pre>

<ol class="wp-block-list" start="7">
  <li>
    打開瀏覽器
  </li>
</ol>

輸入:

<pre class="wp-block-code"><code class="">127.0.0.1:5000</code></pre>

會看到下圖，每次刷新頁面，計數加1:ㄋ  
<img decoding="async" src="https://i.imgur.com/iCAiHPA.png" alt="" /> 

<pre class="wp-block-code"><code class="">Hello Container World! I have been seen 2 times and my hostname is a426b16a8d01.</code></pre>

## 總結 

如果把上面的步驟合併到一起，成為一個部署腳本:

<pre class="wp-block-code"><code class=""># prepare image
docker image pull redis
docker image build -t flask-demo .

# create network
docker network create -d bridge demo-network

# create container
docker container run -d --name redis-server --network demo-network redis
docker container run -d --network demo-network --name flask-demo --env REDIS_HOST=redis-server -p 5000:5000 flask-demo</code></pre>