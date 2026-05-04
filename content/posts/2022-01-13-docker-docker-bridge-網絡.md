---
title: '[Docker] Docker Bridge – 本地練習'
author: Bocky
type: post
date: 2022-01-13T15:11:07+00:00
url: /2022/01/13/docker-docker-bridge-網絡/
categories:
  - Docker
  - Docker-Compose

---
<figure class="wp-block-image"><img decoding="async" src="https://i.imgur.com/jlz3BoV.png" alt="" /></figure> 

建立出來的容器是互相可以ping的。

<ol class="wp-block-list">
  <li>
    pull image
  </li>
</ol>

<pre class="wp-block-code"><code class="">docker image pull busybox</code></pre>



<ol class="wp-block-list" start="2">
  <li>
    建立容器
  </li>
</ol>

<ul class="wp-block-list">
  <li>
    &#8211;rm :容器停止後會自動刪除
  </li>
  <li>
    -name :容器的名字為 box1
  </li>
  <li>
    /bin/sh -c &#8220;While true; do sleep 3600; done&#8221; : 希望執行的命令
  </li>
</ul>

<pre class="wp-block-code"><code class="">docker container run -d --rm --name box1 busybox /bin/sh -c "while true; do sleep 3600; done"</code></pre>



<ol class="wp-block-list" start="3">
  <li>
    檢查容器是否運行中
  </li>
</ol>

<pre class="wp-block-code"><code class="">docker ps</code></pre>



<ol class="wp-block-list" start="4">
  <li>
    進入名為box1的容器
  </li>
</ol>

<pre class="wp-block-code"><code class="">docker exec -it box1 sh</code></pre>



<ol class="wp-block-list" start="5">
  <li>
    查box1的IP
  </li>
</ol>

<pre class="wp-block-code"><code class="">ip a</code></pre>



查看eth0中的IP，如下圖：  
<img decoding="async" src="https://i.imgur.com/cd4Gjan.png" alt="" /> 



<ol class="wp-block-list" start="6">
  <li>
    ping看看box1的ip是否有通
  </li>
</ol>

<pre class="wp-block-code"><code class="">$ ping 172.17.0.2
PING 172.17.0.2 (172.17.0.2): 56 data bytes
Request timeout for icmp_seq 0
Request timeout for icmp_seq 1
Request timeout for icmp_seq 2
Request timeout for icmp_seq 3</code></pre>



<ol class="wp-block-list" start="7">
  <li>
    建立名為box2的新的容器
  </li>
</ol>

<pre class="wp-block-code"><code class="">$ docker container run -d --rm --name box2 busybox /bin/sh -c "while true; do sleep 3600; done"</code></pre>



<ol class="wp-block-list" start="8">
  <li>
    查看目前容器狀況
  </li>
</ol>

<pre class="wp-block-code"><code class="">docker ps</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/GQVQVie.png" alt="" /> </figure> 

<ol class="wp-block-list" start="9">
  <li>
    查看box2的ip
  </li>
</ol>

這次就不進入容器查看，會看到eth0的IP是172.17.0.3

<pre class="wp-block-code"><code class="">docker exec -it box2 ip a</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/01E1hxU.png" alt="" /> </figure> 

<ol class="wp-block-list" start="10">
  <li>
    用box1來ping box2
  </li>
</ol>

<pre class="wp-block-code"><code class="">docker exec -it box1 ping 172.17.0.3</code></pre>

結果如下，看起來是有通的：

<pre class="wp-block-code"><code class="">PING 172.17.0.3 (172.17.0.3): 56 data bytes
64 bytes from 172.17.0.3: seq=0 ttl=64 time=0.159 ms
64 bytes from 172.17.0.3: seq=1 ttl=64 time=0.432 ms
64 bytes from 172.17.0.3: seq=2 ttl=64 time=0.317 ms
64 bytes from 172.17.0.3: seq=3 ttl=64 time=0.384 ms</code></pre>

<ol class="wp-block-list" start="11">
  <li>
    pull image nginx
  </li>
</ol>

<pre class="wp-block-code"><code class="">docker image pull nginx</code></pre>

<ol class="wp-block-list" start="12">
  <li>
    創建名為web1的容器
  </li>
</ol>

<pre class="wp-block-code"><code class="">docker run -d --name web1 nginx</code></pre>

<ol class="wp-block-list" start="13">
  <li>
    查看web1的IP
  </li>
</ol>

<pre class="wp-block-code"><code class="">docker inspect web1</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/Ueid9V0.png" alt="" /> </figure> 

補充：因為web沒有安裝ip的指令，所以使用ip a會跳出錯誤訊息

<pre class="wp-block-code"><code class="">$ docker exec -it web1 ip a
OCI runtime exec failed: exec failed: container_linux.go:380: starting container process caused: exec: "ip": executable file not found in $PATH: unknown</code></pre>

<ol class="wp-block-list" start="14">
  <li>
    測試是否相通
  </li>
</ol>

進入box1的shell

<pre class="wp-block-code"><code class="">docker exec -it box1 sh</code></pre>

<pre class="wp-block-code"><code class="">/ # ping 172.17.0.4
PING 172.17.0.4 (172.17.0.4): 56 data bytes
64 bytes from 172.17.0.4: seq=0 ttl=64 time=0.672 ms
64 bytes from 172.17.0.4: seq=1 ttl=64 time=0.344 ms
64 bytes from 172.17.0.4: seq=2 ttl=64 time=0.307 ms
64 bytes from 172.17.0.4: seq=3 ttl=64 time=0.273 ms</code></pre>

下載172.17.0.4:80的html

<pre class="wp-block-code"><code class="">/ # wget 172.17.0.4:80
Connecting to 172.17.0.4:80 (172.17.0.4:80)
saving to 'index.html'
index.html           100% |*************************************************************************|   615  0:00:00 ETA
'index.html' saved</code></pre>

查看html檔案

<pre class="wp-block-code"><code class="">cat index.html</code></pre>

<ol class="wp-block-list" start="15">
  <li>
    端口轉發
  </li>
</ol>

建立一個新的container，將80轉到local

<pre class="wp-block-code"><code class="">docker run -d -p 80:80 --name web2 nginx</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/ab1GUCU.png" alt="" /> </figure> 

<ol class="wp-block-list" start="16">
  <li>
    測試是否有分享到本機
  </li>
</ol>

開啟瀏覽器，輸入:

<pre class="wp-block-code"><code class="">127.0.0.1:80</code></pre>

如果有成功將web2的nginx的80port分享來，會顯示：

<pre class="wp-block-code"><code class="">Welcome to nginx!
If you see this page, the nginx web server is successfully installed and working. Further configuration is required.

For online documentation and support please refer to nginx.org.
Commercial support is available at nginx.com.

Thank you for using nginx.</code></pre>