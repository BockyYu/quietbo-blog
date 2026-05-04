---
title: '[Mac|M1] Port 5000 already in use,Port 5000一直被佔用(已解決)'
author: Bocky
type: post
date: 2022-01-21T20:00:38+00:00
url: /2022/01/22/macm1-port-5000-already-in-useport-5000一直被佔用已解決/
categories:
  - 系統相關
tags:
  - mac

---
再學習docker+flask+redis時遇到一個小問題，就是5000一直被佔用著，但Flask 預設使用 port 5000。

查詢port 5000是否被佔用:

<pre class="wp-block-code"><code class="">$ sudo lsof -i :5000
COMMAND     PID  USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
ControlCe 96400 bocky   36u  IPv4 0xb3652d5dff6c5fe3      0t0  TCP *:commplex-main (LISTEN)
ControlCe 96400 bocky   37u  IPv6 0xb3652d5dec3e630b      0t0  TCP *:commplex-main (LISTEN)</code></pre>

查詢結果已經在使用了

## 解決方式1. 

左上角[系統偏好設定]<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/8Tv4FHr.png" alt="" /> </figure> 

點擊[共享]  
<img decoding="async" src="https://i.imgur.com/L7TRWPJ.png" alt="" /> 

將AirPlay接收器關閉。  
<img decoding="async" src="https://i.imgur.com/umGw5mx.png" alt="" /> 

## 解決方式2. 

將flask更換其他port號，更換port方式請自行搜尋。