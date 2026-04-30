---
title: '[Docker-compose] 安裝'
author: Bocky
type: post
date: 2022-01-23T15:01:47+00:00
url: /2022/01/23/docker-compose-安裝/
categories:
  - 'Docker&amp; Docker-compose'
tags:
  - docker-compose

---
<ol class="wp-block-list">
  <li>
    Mac在默認安裝了docker desktop以後，docker-compose隨之自動安裝，直接下指令來查詢目前docker-compose的版本:
  </li>
</ol>

<pre class="wp-block-code"><code class="">$ docker-compose --version
docker-compose version 1.29.2, build 5becea4c</code></pre>

<ol class="wp-block-list" start="2">
  <li>
    Linux用戶需要自行安裝
  </li>
</ol>

最新版本號可以在這裡查詢:[GitHub][1]

<pre class="wp-block-code"><code class="">$ sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
$ docker-compose --version
docker-compose version 1.29.2, build 5becea4c</code></pre>

<ol class="wp-block-list" start="3">
  <li>
    使用python的用戶，可以使用pip去安裝docker-Compose
  </li>
</ol>

<pre class="wp-block-code"><code class="">pip install docker-compose</code></pre>

 [1]: https://github.com/docker/compose/releases