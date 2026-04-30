---
title: '[Docker] 80port被佔用。Error response from daemon: driver failed programming external connectivity on endpoint cranky_banzai(解決)'
author: Bocky
type: post
date: 2022-06-07T10:23:23+00:00
url: /2022/06/07/docker-80port被佔用。error-response-from-daemon-driver-failed-programming-external-connectivity-on-endpoint-cranky_banzai解決/
categories:
  - 'Docker&amp; Docker-compose'
tags:
  - docker

---
當我在docker創建containerd時, 出現被佔用訊息, 如下:

<pre class="wp-block-code"><code class="">docker: Error response from daemon: driver failed programming external connectivity on endpoint cranky_banzai (6e53d887b7e49120d6eb6d061196c5f4edd36e5527a9554dfed718184081a0a2): Error starting userland proxy: listen tcp4 0.0.0.0:80: bind: address already in use.</code></pre>

網路上很多都是把docker restart就解決了, 如果沒解決, 可能是被其他佔用了。

執行:

<pre class="wp-block-code"><code class="">netstat | grep 80</code></pre>

沒看到80被佔用。  
<img decoding="async" src="https://i.imgur.com/7pG0p48.png" alt="" /> 

<pre class="wp-block-code"><code class="">netstat -tulpn | grep :80</code></pre>

(Not all processes could be identified, non-owned process info  
will not be shown, you would have to be root to see it all.)

<pre class="wp-block-code"><code class="">tcp6       0      0 :::80                   :::*                    LISTEN      -</code></pre>

看起來是有東西, 但必須使用root才能知道是什麼，切換成root後再看一次

<pre class="wp-block-code"><code class="">sudo su -
netstat -tulpn | grep :80</code></pre>

看到是LISTEN 858230/apache2  
因為我沒有在使用apache2所以我就先停掉。

  
<img decoding="async" src="https://i.imgur.com/HyPa2tQ.png" alt="" /> 

<pre class="wp-block-code"><code class="">sudo /etc/init.d/apache2 stop</code></pre><figure class="wp-block-image is-style-default">

<img decoding="async" src="https://i.imgur.com/d4sSrIr.png" alt="" /> </figure> 

離開root

<pre class="wp-block-code"><code class="">exit</code></pre>

再執行一次docker run -d -p 80:80 nginx  
成功解決這次被佔用問題!