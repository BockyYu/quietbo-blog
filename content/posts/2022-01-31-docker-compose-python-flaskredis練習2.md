---
title: '[Docker-compose] Python Flask+Redis(練習2)'
author: Bocky
type: post
date: 2022-01-31T12:28:54+00:00
url: /2022/01/31/docker-compose-python-flaskredis練習2/
categories:
  - 'Docker&amp; Docker-compose'
tags:
  - docker-compose

---
yml的基本語法結構:

<pre class="wp-block-code"><code class="">services: # 容器
  servicename: # 服務名字，這個名字也是內部 bridge網絡可以使用的 DNS name
    image: # 鏡像的名字
    command: # 可選，如果設置，則會覆蓋默認鏡像裡的 CMD命令
    environment: # 可選，相當於 docker run裡的 --env
    volumes: # 可選，相當於docker run裡的 -v
    networks: # 可選，相當於 docker run裡的 --network
    ports: # 可選，相當於 docker run裡的 -p
  servicename2:

volumes: # 可選，相當於 docker volume create

networks: # 可選，相當於 docker network create</code></pre>

<ul class="wp-block-list">
  <li>
    services<br />對照:<a href="https://docs.docker.com/compose/compose-file/">Compose and Docker compatibility</a>
  </li>
  <li>
    servicename<br />與前一篇在docker時下指令的&#8211;name flask-demo 一致
  </li>
</ul>

## 練習 {#練習.wp-block-heading}

以[Python Flask+Redis(練習)][1]：為例子，改造成一個docker-compose文件

app.py檔案內容如下:

<pre class="wp-block-code"><code class="">from flask import Flask

app = Flask(__name__)


@app.route('/')
def hello_world():
    return 'hello'


if __name__ == "__main__":
    app.run(debug=True, host='0.0.0.0', port=5000)</code></pre>

dockerfile如下：

<pre class="wp-block-code"><code class="">FROM python:3.9.5-slim

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

docker-compose.yml內容如下:

<pre class="wp-block-code"><code class="">version: "3.8"

services:
  flask-demo:
    image: flask-demo:latest
    environment:
      - REDIS_HOST=redis-server
    networks:
      - demo-network
    ports:
      - 8899:5000

  redis-server:
    image: redis:latest
    networks:
      - demo-network

networks:
  demo-network: null</code></pre>

<ol class="wp-block-list">
  <li>
    資料結構
  </li>
</ol>

<pre class="wp-block-code"><code class="">.
├── app.py
├── docker-compose.yml
└── dockerfile</code></pre>

<ol class="wp-block-list" start="2">
  <li>
    建立2個image
  </li>
</ol>

<ul class="wp-block-list">
  <li>
    下載redis image
  </li>
</ul>

<pre class="wp-block-code"><code class="">docker image pull redis</code></pre>

<ul class="wp-block-list">
  <li>
    建立flask-demo的image
  </li>
</ul>

<pre class="wp-block-code"><code class="">docker image build -t flask-demo .</code></pre>

<ol class="wp-block-list" start="3">
  <li>
    運行docker-compose
  </li>
</ol>

<pre class="wp-block-code"><code class="">$ docker-compose up  
Creating network "my_flask_demo-network" with the default driver
Creating my_flask_redis-server_1 ... done
Creating my_flask_flask-demo_1   ... done
Attaching to my_flask_redis-server_1, my_flask_flask-demo_1
redis-server_1  | 1:C 31 Jan 2022 12:26:05.447 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
redis-server_1  | 1:C 31 Jan 2022 12:26:05.447 # Redis version=6.2.6, bits=64, commit=00000000, modified=0, pid=1, just started
redis-server_1  | 1:C 31 Jan 2022 12:26:05.447 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
redis-server_1  | 1:M 31 Jan 2022 12:26:05.447 * monotonic clock: POSIX clock_gettime
redis-server_1  | 1:M 31 Jan 2022 12:26:05.448 * Running mode=standalone, port=6379.
redis-server_1  | 1:M 31 Jan 2022 12:26:05.448 # Server initialized
redis-server_1  | 1:M 31 Jan 2022 12:26:05.449 * Ready to accept connections
flask-demo_1    |  * Serving Flask app 'app.py' (lazy loading)
flask-demo_1    |  * Environment: production
flask-demo_1    |    WARNING: This is a development server. Do not use it in a production deployment.
flask-demo_1    |    Use a production WSGI server instead.
flask-demo_1    |  * Debug mode: off
flask-demo_1    |  * Running on all addresses.
flask-demo_1    |    WARNING: This is a development server. Do not use it in a production deployment.
flask-demo_1    |  * Running on http://172.25.0.3:5000/ (Press CTRL+C to quit)</code></pre>

打開瀏覽器輸入  
127.0.0.1:8899<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/pES3Goo.png" alt="" /> </figure>

 [1]: https://quietbo.com/2022/01/22/docker-mac-python-flaskredis%e7%b7%b4%e7%bf%92/