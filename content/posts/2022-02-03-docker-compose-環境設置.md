---
title: '[docker-compose] 環境設置'
author: Bocky
type: post
date: 2022-02-03T13:08:42+00:00
url: /2022/02/03/docker-compose-環境設置/
categories:
  - Docker
  - Docker-Compose
tags:
  - docker-compose

---
主要docker-compose.yml檔案不要直接暴露redis的密碼。

## 使用.env設置密碼範例 {#使用-env設置密碼範例.wp-block-heading}

下方為目錄結構:<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/1mLAJkZ.png" alt="" /> </figure> 

以下為docker-compose.yml檔內容

<pre class="wp-block-code"><code lang="docker" class="language-docker line-numbers">version: "3.8"

services:
  flask:
    build:
      context: ./flask
      dockerfile: Dockerfile
    image: flask-demo:latest
    environment:
      - REDIS_HOST=redis-server
      - REDIS_PASS=${REDIS_PASS}
    networks:
      - backend
      - frontend

  redis-server:
    image: redis:latest
    command: redis-server --requirepass ${REDIS_PASS}
    networks:
      - backend

  nginx:
    image: nginx:stable-alpine
    ports:
      - 8000:80
    depends_on:
      - flask
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/conf.d/default.conf:ro
      - ./var/log/nginx:/var/log/nginx
    networks:
      - frontend

networks:
  backend:
  frontend:</code></pre>

.env檔

<pre class="wp-block-code"><code class="">REDIS_PASS=ABC123</code></pre>

.gitignore檔(用於不要上傳到git上)

<pre class="wp-block-code"><code class="">.env</code></pre>

查看目前設置內容:

<pre class="wp-block-code"><code class="">docker-compose config</code></pre>

## 指定路徑的方式 {#指定路徑的方式.wp-block-heading}

若不使用.env檔，想使用其他路徑下的檔案，改成myenv的檔名，下指令

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">docker-compose --env-file myenv config
docker-compose --env-file myenv up -d</code></pre>

則可正常執行。