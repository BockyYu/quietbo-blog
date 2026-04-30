---
title: '[Docker] Data Volume的練習(MySQL)'
author: Bocky
type: post
date: 2022-01-10T15:05:46+00:00
url: /2022/01/10/docker-data-volume的練習mysql/
categories:
  - 'Docker&amp; Docker-compose'
tags:
  - docker

---
<ul class="wp-block-list">
  <li>
    MAC M1
  </li>
</ul>

<ol class="wp-block-list">
  <li>
    下載Mysql 5.7的image
  </li>
</ol>

<pre class="wp-block-code"><code class="">docker pull --platform linux/amd64 mysql:5.7</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/998OIK4.png" alt="" /> </figure> 

<ol class="wp-block-list" start="2">
  <li>
    使用剛才下載的image創建出容器，並將mysql的密碼設為123456
  </li>
</ol>

<pre class="wp-block-code"><code class="">docker container run --name some-mysql -e MYSQL_ROOT_PASSWORD=123456 -d -v mysql-data:/var/lib/mysql mysql:5.7
docker container ls</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/wh0ZN2C.png" alt="" /> </figure> <figure class="wp-block-image"><img decoding="async" src="https://i.imgur.com/gdHrOxc.png" alt="" /></figure> 

<pre class="wp-block-code"><code class="">docker volume ls
docker volume inspect mysql-data</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/kOypCQi.png" alt="" /> </figure> 

<ol class="wp-block-list" start="3">
  <li>
    進入container，下方的71f請更換成自己的container id
  </li>
</ol>

<pre class="wp-block-code"><code class="">docker exec -it containerId sh</code></pre>

進入後再進入MySQL，密碼為剛剛的123456

<pre class="wp-block-code"><code class="">mysql -u root -p</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/MansRUm.png" alt="" /> </figure> 

<ol class="wp-block-list" start="4">
  <li>
    創建一個database(最後要用;來結尾)
  </li>
</ol>

<pre class="wp-block-code"><code class="">show databases;
create database demo;
show databases;</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/Ej9yBrq.png" alt="" /> </figure> 

<ol class="wp-block-list" start="5">
  <li>
    確認有建立demo後，離開mysql和container
  </li>
</ol>

使用2次exit來離開。  
<img decoding="async" src="https://i.imgur.com/a4c23zv.png" alt="" /> <figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/dRlrRCF.png" alt="" /> </figure> 

查看文件夾可參考這篇[[Docker] Mac M1 – no such file or directory: /var/lib/docker/volumes ，找不到var/lib/docker/volumes (已解決)][1]

<ol class="wp-block-list" start="6">
  <li>
    刪除container
  </li>
</ol>

<pre class="wp-block-code"><code class="">docker container ls
docker container rm -f containerId</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/Rcsnl4M.png" alt="" /> </figure> 

<ol class="wp-block-list" start="7">
  <li>
    查看volume是否還在
  </li>
</ol><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/Ih097ha.png" alt="" /> </figure> 

<ol class="wp-block-list" start="8">
  <li>
    再創建一個已經存在的volume
  </li>
</ol>

雖然這指令跟第二步驟是一樣的，但因為紅框內還是我們volume的路徑，所以資料會繼續沿用。

<pre class="wp-block-code"><code class="">docker container run --name some-mysql -e MYSQL_ROOT_PASSWORD=123456 -d -v mysql-data:/var/lib/mysql mysql:5.7</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/45Tcpk1.png" alt="" /> </figure> 

<ol class="wp-block-list" start="9">
  <li>
    進入container查看mysql的資料，會看到原本創建的demo。<br /><img decoding="async" src="https://i.imgur.com/B5JetIt.png" alt="" />
  </li>
</ol>

 [1]: https://quietbo.com/2021/12/23/docker-mac-m1-no-such-file-or-directory-var-lib-docker-volumes-%ef%bc%8c%e6%89%be%e4%b8%8d%e5%88%b0var-lib-docker-volumes-%e5%b7%b2%e8%a7%a3%e6%b1%ba/