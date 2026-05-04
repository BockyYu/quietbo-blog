---
title: '[Docker] volume 指定/ 不指定-v参数'
author: Bocky
type: post
date: 2022-01-10T16:21:51+00:00
url: /2022/01/11/docker-volume-指定-不指定-v参数/
categories:
  - 'Docker&amp; Docker-compose'

---
下方為dockerfile的內容

<pre class="wp-block-code"><code class="">FROM alpine:latest
RUN apk update
RUN apk --no-cache add curl
ENV SUPERCRONIC_URL=https://github.com/aptible/supercronic/releases/download/v0.1.12/supercronic-linux-amd64 \
    SUPERCRONIC=supercronic-linux-amd64 \
    SUPERCRONIC_SHA1SUM=048b95b48b708983effb2e5c935a1ef8483d9e3e
RUN curl -fsSLO "$SUPERCRONIC_URL" \
    && echo "${SUPERCRONIC_SHA1SUM}  ${SUPERCRONIC}" | sha1sum -c - \
    && chmod +x "$SUPERCRONIC" \
    && mv "$SUPERCRONIC" "/usr/local/bin/${SUPERCRONIC}" \
    && ln -s "/usr/local/bin/${SUPERCRONIC}" /usr/local/bin/supercronic
COPY my-cron /app/my-cron
WORKDIR /app

VOLUME ["/app"]

# RUN cron job
CMD ["/usr/local/bin/supercronic", "/app/my-cron"]</code></pre>

<ol class="wp-block-list">
  <li>
    構建鏡像<br />在終端機執行：
  </li>
</ol>

<pre class="wp-block-code"><code class="">docker image build -t my-cron .
docker image ls</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/MquvGsa.png" alt="" /> </figure> 

<ol class="wp-block-list" start="2">
  <li>
    創建容器(不指定-v參數)
  </li>
</ol>

<pre class="wp-block-code"><code class="">docker run -d my-cron
docker volume ls</code></pre>

此時Docker會自動創建一個隨機名字的volume，存儲在Dockerfile定義的volume

<pre class="wp-block-code"><code class="">VOLUME ["/app"]</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/Flj1Mdr.png" alt="" /> </figure> <figure class="wp-block-image"><img decoding="async" src="https://i.imgur.com/0gKd2fc.png" alt="" /></figure> 

## 創建容器(指定-v參數) 

在創建容器的時候通過 -v 參數，我們可以手動的指定**需要創建Volume的名字**，以及**對應於容器內的路徑**，這個路徑是可以任意的，不必需要在Dockerfile裡通過VOLUME來定義。

把原本Dockerfile裡的VOLUME刪除(如下)

<pre class="wp-block-code"><code class="">FROM alpine:latest
RUN apk update
RUN apk --no-cache add curl
ENV SUPERCRONIC_URL=https://github.com/aptible/supercronic/releases/download/v0.1.12/supercronic-linux-amd64 \
    SUPERCRONIC=supercronic-linux-amd64 \
    SUPERCRONIC_SHA1SUM=048b95b48b708983effb2e5c935a1ef8483d9e3e
RUN curl -fsSLO "$SUPERCRONIC_URL" \
    && echo "${SUPERCRONIC_SHA1SUM}  ${SUPERCRONIC}" | sha1sum -c - \
    && chmod +x "$SUPERCRONIC" \
    && mv "$SUPERCRONIC" "/usr/local/bin/${SUPERCRONIC}" \
    && ln -s "/usr/local/bin/${SUPERCRONIC}" /usr/local/bin/supercronic
COPY my-cron /app/my-cron
WORKDIR /app

# RUN cron job
CMD ["/usr/local/bin/supercronic", "/app/my-cron"]</code></pre>

重新build鏡像，然後創建容器，加-v參數:

<pre class="wp-block-code"><code class="">docker image build -t my-cron .
docker container run -d -v cron-data:/app my-cron
docker volume ls
docker volume inspect cron-data  </code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/HSkWhf0.png" alt="" /> </figure> 

## 環境清理 

強制刪除所有容器，系統清理和volume清理

<pre class="wp-block-code"><code class="">docker rm -f $(docker container ps -aq)
docker system prune -f
docker volume prune -f</code></pre>