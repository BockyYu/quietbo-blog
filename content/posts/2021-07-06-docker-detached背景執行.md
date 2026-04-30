---
title: '[Docker] Run container in the background – detached背景執行'
author: Bocky
type: post
date: 2021-07-05T19:17:38+00:00
url: /2021/07/06/docker-detached背景執行/
categories:
  - 'Docker&amp; Docker-compose'
tags:
  - docker

---
本機:mac M1 11.2.3  
docker: 20.10.7

先讓容器在背景保持運作中，不進入shell介面。

<ul class="wp-block-list">
  <li>
    run 是pull(下載 image) 和 create（創建容器）和 start（啟動容器）組合在一起的功能。
  </li>
  <li>
    -d 代表 detach，將docker在背景執行。
  </li>
  <li>
    -p 80:80是將主機的80port轉到web這個Container的80 port。
  </li>
</ul>

<pre class="wp-block-code"><code lang="docker" class="language-docker line-numbers">docker run -d -p 80:80 nginx
docker ps -a</code></pre>

建立完後會跳出一串英數的字串，這是CONTAINER ID，顯示完就會直接回來，且不會卡在shell。<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/iWcc1M4.png" alt="" /> </figure> 

用本機的瀏覽器打開網頁，輸入127.0.0.1會看到下圖。  
<img decoding="async" src="https://i.imgur.com/Ev40ddq.png" alt="" /> 

回到終端機，會看到終端機還是維持原本的畫面，但正常來說只要有進到網頁，就會有log，如果想要看到log的話，就可以輸入：

<pre class="wp-block-code"><code lang="docker" class="language-docker">docker container logs CONTAINER_ID</code></pre>

這樣就會印出該container的log。  
<img decoding="async" src="https://i.imgur.com/3uYrAXB.png" alt="" /> 

但這樣也很麻煩，因為想看log的話就要一直來下指令，下方為自動顯示log的指令：

<pre class="wp-block-code"><code lang="docker" class="language-docker">docker container logs -f CONTAINER_ID</code></pre>

若是在這時候使用control+C的話，不會將container關閉。  
<img decoding="async" src="https://i.imgur.com/R8MUnzJ.png" alt="" /> 

下方指令用attach來連接運行中的container。  
回到container的shell，之後的log會顯示出來。（如果想看之前的紀錄就開另一個終端機去執行logs)

<pre class="wp-block-code"><code lang="docker" class="language-docker">docker attach CONTAINER_ID</code></pre>

在attach時使用`control+C`就直接被關閉。  
<img decoding="async" src="https://i.imgur.com/9NaYIbX.png" alt="" />