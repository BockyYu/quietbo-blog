---
title: '[Redis]安裝'
author: Bocky
type: post
date: 2021-03-24T08:00:54+00:00
url: /2021/03/24/redis-server-安裝/
categories:
  - Redis
tags:
  - 安裝

---
利用apt套件管理器安裝:

<pre class="wp-block-code"><code lang="bash" class="language-bash">sudo apt update
sudo apt install redis-server -y</code></pre>

檢查redis服務狀態:  
安裝完應會自動啟動。開啟會出現綠色字active(running)  
<img decoding="async" src="https://i.imgur.com/bSzwVOX.png" alt="" /> 

檢查服務狀態:

<pre class="wp-block-code"><code lang="bash" class="language-bash">service redis-server status </code></pre>

停止redis server:

<pre class="wp-block-code"><code lang="bash" class="language-bash">service redis-server stop</code></pre>

啟動redis server:

<pre class="wp-block-code"><code lang="bash" class="language-bash">service redis-server start</code></pre>

啟動redis服務器:

<pre class="wp-block-code"><code lang="bash" class="language-bash">redis-cli</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/KUEm3J5.png" alt="" /> </figure>