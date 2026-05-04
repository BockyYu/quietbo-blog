---
title: '[Docker] –network host, None'
author: Bocky
type: post
date: 2022-01-17T15:17:52+00:00
url: /2022/01/17/docker-network-host-none/
categories:
  - 'Docker&amp; Docker-compose'
tags:
  - docker

---
 

環境：Linux

注意：  
主機網絡驅動程序僅適用於 Linux 主機，不支持 Docker Desktop for Mac、Docker Desktop for Windows 或 Docker EE for Windows Server。  
<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/OJh6RUm.png" alt="" /> </figure> 

## &#8211;network host 

創建4個容器:

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">docker run -d --name web1 nginx
docker run -d --name web2 nginx
docker run -d --name web3 nginx
docker run -d --name web4 --network host nginx</code></pre>

都是監聽80的port  
<img decoding="async" src="https://i.imgur.com/R15HOJ9.png" alt="" /> 

打開瀏覽器輸入127.0.0.1  
能夠成功看到nginx的頁面，而這個頁面是由web4與本地連接的，並非we1,web2,web3，若是想要再創建一個web5，則無法創建。

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">docker run -d --name web5 --network host nginx
docker logs -f web5</code></pre>

原因是80的port已被佔用。

<pre class="wp-block-code"><code class="">bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)</code></pre>

## &#8211;network none 

無法對內，對外進行通訊

<pre class="wp-block-code"><code class="">$ docker exec -it box1 ip a
1: lo: &lt;LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: tunl0@NONE: &lt;NOARP> mtu 1480 qdisc noop qlen 1000
    link/ipip 0.0.0.0 brd 0.0.0.0
3: ip6tnl0@NONE: &lt;NOARP> mtu 1452 qdisc noop qlen 1000
    link/tunnel6 00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00 brd 00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00

</code></pre>