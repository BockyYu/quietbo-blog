---
title: '[docker-compose] image build與pull(build非dockerfile名稱)'
author: Bocky
type: post
date: 2022-02-01T13:52:15+00:00
url: /2022/02/01/docker-compose-image-build與pullbuild非dockerfile名稱/
categories:
  - 'Docker&amp; Docker-compose'
tags:
  - docker-compose

---
 

<div id="ez-toc-container" class="ez-toc-v2_0_82_2 ez-toc-wrap-center counter-hierarchy ez-toc-counter ez-toc-grey ez-toc-container-direction">
  <div class="ez-toc-title-container">
    <p class="ez-toc-title" style="cursor:inherit">
      Table of Contents
    </p>
    
    <span class="ez-toc-title-toggle"><a href="#" class="ez-toc-pull-right ez-toc-btn ez-toc-btn-xs ez-toc-btn-default ez-toc-toggle" aria-label="顯示/隱藏內容目錄"><span class="ez-toc-js-icon-con"><span class=""><span class="eztoc-hide" style="display:none;">Toggle</span><span class="ez-toc-icon-toggle-span"><svg style="fill: #999;color:#999" xmlns="http://www.w3.org/2000/svg" class="list-377408" width="20px" height="20px" viewBox="0 0 24 24" fill="none"><path d="M6 6H4v2h2V6zm14 0H8v2h12V6zM4 11h2v2H4v-2zm16 0H8v2h12v-2zM4 16h2v2H4v-2zm16 0H8v2h12v-2z" fill="currentColor"></path></svg><svg style="fill: #999;color:#999" class="arrow-unsorted-368013" xmlns="http://www.w3.org/2000/svg" width="10px" height="10px" viewBox="0 0 24 24" version="1.2" baseProfile="tiny"><path d="M18.2 9.3l-6.2-6.3-6.2 6.3c-.2.2-.3.4-.3.7s.1.5.3.7c.2.2.4.3.7.3h11c.3 0 .5-.1.7-.3.2-.2.3-.5.3-.7s-.1-.5-.3-.7zM5.8 14.7l6.2 6.3 6.2-6.3c.2-.2.3-.5.3-.7s-.1-.5-.3-.7c-.2-.2-.4-.3-.7-.3h-11c-.3 0-.5.1-.7.3-.2.2-.3.5-.3.7s.1.5.3.7z"/></svg></span></span></span></a></span>
  </div><nav>
  
  <ul class='ez-toc-list ez-toc-list-level-1 ' >
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2022/02/01/docker-compose-image-build%e8%88%87pullbuild%e9%9d%9edockerfile%e5%90%8d%e7%a8%b1/#%E7%9B%AE%E9%8C%84%E7%B5%90%E6%A7%8B" >目錄結構</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2022/02/01/docker-compose-image-build%e8%88%87pullbuild%e9%9d%9edockerfile%e5%90%8d%e7%a8%b1/#docker-compose_image_buildpull%E7%9A%84%E6%8C%87%E4%BB%A4%E5%B7%AE%E7%95%B0" >docker-compose image build/pull的指令差異</a><ul class='ez-toc-list-level-3' >
        <li class='ez-toc-heading-level-3'>
          <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2022/02/01/docker-compose-image-build%e8%88%87pullbuild%e9%9d%9edockerfile%e5%90%8d%e7%a8%b1/#docker-compose_build" >docker-compose build</a>
        </li>
        <li class='ez-toc-page-1 ez-toc-heading-level-3'>
          <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2022/02/01/docker-compose-image-build%e8%88%87pullbuild%e9%9d%9edockerfile%e5%90%8d%e7%a8%b1/#docker-compose_pull" >docker-compose pull</a>
        </li>
      </ul>
    </li>
    
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-5" href="https://quietbo.com/2022/02/01/docker-compose-image-build%e8%88%87pullbuild%e9%9d%9edockerfile%e5%90%8d%e7%a8%b1/#%E9%83%A8%E5%88%86%E5%9F%BA%E7%A4%8E%E7%9A%84%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8" >部分基礎的命令行基本使用</a>
    </li>
  </ul></nav>
</div>

## <span class="ez-toc-section" id="%E7%9B%AE%E9%8C%84%E7%B5%90%E6%A7%8B"></span>目錄結構<span class="ez-toc-section-end"></span> {#目錄結構.wp-block-heading}

當要build的image名稱不是dockerfile時，是其他名稱，且在不同路徑下，例如：

<pre class="wp-block-code"><code class="">.
├── docker-compose.yml
└── my_flask
    ├── app.py
    └── dockerfile.data</code></pre>

<ul class="wp-block-list">
  <li>
    build: 要build的指令：<ul>
      <li>
        context: 檔案路徑
      </li>
      <li>
        dockerfile: 檔案名稱
      </li>
    </ul>
  </li>
</ul>

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

docker_compose.yml檔如下:

<pre class="wp-block-code"><code lang="docker" class="language-docker line-numbers">version: "3.8"

services:
  flask-demo:
    build:
      context: ./my_flask
      dockerfile: Dockerfile.data
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

成功畫面:  
<img decoding="async" src="https://i.imgur.com/9wRyaGQ.png" alt="" /> 

## <span class="ez-toc-section" id="docker-compose_image_buildpull%E7%9A%84%E6%8C%87%E4%BB%A4%E5%B7%AE%E7%95%B0"></span>docker-compose image build/pull的指令差異<span class="ez-toc-section-end"></span> {#docker-compose-image-build-pull的指令差異.wp-block-heading}

當docker-compose.yml檔內同時有要從dockerfile build的image與從dockerhub pull下來時，這兩種會不同結果

### <span class="ez-toc-section" id="docker-compose_build"></span>docker-compose build<span class="ez-toc-section-end"></span> {#docker-compose-build.wp-block-heading}

下方是利用docker_compose.yml檔執行的結果，只有build dockerfile，沒有redis image：<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/0WtFnrJ.png" alt="" /> </figure> 

### <span class="ez-toc-section" id="docker-compose_pull"></span>docker-compose pull<span class="ez-toc-section-end"></span> {#docker-compose-pull.wp-block-heading}

下方是從dockerhub pull redis，因為dockerfile的關係所以馬上就是done，而pull則需等待下載:<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/oM8hTaq.png" alt="" /> </figure> 

可以看到，下方使用pull，只有一個redis的image<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/eeXIX8v.png" alt="" /> </figure> 

## <span class="ez-toc-section" id="%E9%83%A8%E5%88%86%E5%9F%BA%E7%A4%8E%E7%9A%84%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8"></span>部分基礎的命令行基本使用<span class="ez-toc-section-end"></span> {#部分基礎的命令行基本使用.wp-block-heading}

<ul class="wp-block-list">
  <li>
    -d: 背景執行
  </li>
</ul>

<pre class="wp-block-code"><code class="">docker-compose up -d</code></pre>

若想查看log可使用下方兩個指令

<ul class="wp-block-list">
  <li>
    -f :持續動態的查看
  </li>
</ul>

<pre class="wp-block-code"><code class="">docker-compose logs
docker-compose logs -f</code></pre>

查看容器目前狀況:

<pre class="wp-block-code"><code class="">$ docker-compose ps
         Name                        Command               State           Ports         
-----------------------------------------------------------------------------------------
my_flask_flask-demo_1     flask run -h 0.0.0.0             Up      0.0.0.0:8899-&gt;5000/tcp
my_flask_redis-server_1   docker-entrypoint.sh redis ...   Up      6379/tcp      </code></pre>

注意:使用docker-compose ps時，要在yml檔的目錄底下才能使用，否則無法查詢

將容器停止:

<pre class="wp-block-code"><code class="">docker-compose stop</code></pre>

將已經停止的容器刪除:

<pre class="wp-block-code"><code class="">$ docker-compose rm  
Going to remove my_flask_flask-demo_1, my_flask_redis-server_1
Are you sure? [yN] y
Removing my_flask_flask-demo_1   ... done
Removing my_flask_redis-server_1 ... done</code></pre>