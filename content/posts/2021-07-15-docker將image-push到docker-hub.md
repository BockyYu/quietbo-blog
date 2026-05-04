---
title: '[Docker]將Image push到Docker Hub'
author: Bocky
type: post
date: 2021-07-14T18:53:19+00:00
url: /2021/07/15/docker將image-push到docker-hub/
categories:
  - Docker
  - Docker-Compose
tags:
  - docker

---
<ol class="wp-block-list">
  <li>
    需要<a href="https://hub.docker.com/">docker hub</a>的帳號
  </li>
  <li>
    開啟終端機，輸入下方指令後輸入帳號密碼，成功則顯示：Login Succeeded
  </li>
</ol>

<pre class="wp-block-code"><code lang="docker" class="language-docker">docker login</code></pre>

<ol class="wp-block-list" start="3">
  <li>
    建立新的tag<br />把原本的hello(藍框)建立新的tag，主要是push到docker hub的格式，但這兩個是同一個鏡像(IMAGE ID)
  </li>
</ol>

<pre class="wp-block-code"><code lang="docker" class="language-docker">docker tag hello {dockerHub帳號}/hello:1.0</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/dcmznsP.png" alt="" /> </figure> 

<ol class="wp-block-list" start="4">
  <li>
    push到docker hub
  </li>
</ol>

<pre class="wp-block-code"><code lang="docker" class="language-docker">docker image push {dockerHub的帳號}/hello:1.0</code></pre>

執行成功如下圖：  
<img decoding="async" src="https://i.imgur.com/cuI2tXC.png" alt="" />  
到docker hub查看是否有push成功。  
<img decoding="async" src="https://i.imgur.com/quOgzQq.png" alt="" /> 

<ol class="wp-block-list" start="5">
  <li>
    拉取剛才push的image:<br />先刪除原本push的image，沒有的話再pull剛剛傳上去的image
  </li>
</ol>

<pre class="wp-block-code"><code lang="docker" class="language-docker">docker pull dockerHub的帳號/hello:1.0</code></pre>

用docker image ls 查看pull的image是否成功  
<img decoding="async" src="https://i.imgur.com/okiWOQY.png" alt="" />