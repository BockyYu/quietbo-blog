---
title: '[Docker] dockerfile端口轉發'
author: Bocky
type: post
date: 2022-01-17T14:21:35+00:00
url: /2022/01/17/docker-dockerfile端口轉發/
categories:
  - 'Docker&amp; Docker-compose'
tags:
  - docker

---
## pull image 

先pull兩個image:  
python:3.9.5-slim

<pre class="wp-block-code"><code lang="bash" class="language-bash">docker image pull python:3.9.5-slim</code></pre>

redis

<pre class="wp-block-code"><code lang="bash" class="language-bash">docker image pull redis</code></pre>

新增2個dockerfile

<pre class="wp-block-code"><code lang="docker" class="language-docker line-numbers">FROM python:3.9.5-slim

RUN pip install flask redis && \
    groupadd -r flask && useradd -r -g flask flask && \
    mkdir /src && \
    chown -R flask:flask /src

USER flask

COPY startup.py /src/startup.py

WORKDIR /src

ENV FLASK_APP=startup.py REDIS_HOST=redis

#EXPOSE 5000

CMD ["flask", "run", "-h", "0.0.0.0"]</code></pre>

用上方的dockerfile build image，註解掉EXPOSE的image名為flask-demo：

<pre class="wp-block-code"><code lang="bash" class="language-bash">docker image build -t flask-demo .</code></pre>

再建立一個image，這個image只是把EXPOSE 5000打開。

<pre class="wp-block-code"><code lang="docker" class="language-docker line-numbers">FROM python:3.9.5-slim

RUN pip install flask redis && \
    groupadd -r flask && useradd -r -g flask flask && \
    mkdir /src && \
    chown -R flask:flask /src

USER flask

COPY startup.py /src/startup.py

WORKDIR /src

ENV FLASK_APP=startup.py REDIS_HOST=redis

EXPOSE 5000

CMD ["flask", "run", "-h", "0.0.0.0"]</code></pre>

打開EXPOSE的image名為flask-demo-new。

<pre class="wp-block-code"><code lang="bash" class="language-bash">docker image build -t flask-demo-new .</code></pre>

建立後查看image

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">docker image inspect flask-demo
docker image inspect flask-demo-new</code></pre>

裡面的Config只有flask-demo-new的有多出

<pre class="wp-block-code"><code class="">"ExposedPorts": {
                "5000/tcp": {}
            },</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/jvFogBK.png" alt="" /> </figure>