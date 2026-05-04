---
title: '[Docker] Mac M1 – no matching manifest for linux/arm64/v8 in the manifest list entries(已解決)'
author: Bocky
type: post
date: 2021-09-27T13:47:30+00:00
url: /2021/09/27/docker-mac-m1-no-matching-manifest-for-linux-arm64-v8-in-the-manifest-list-entries已解決/
categories:
  - Docker
  - Docker-Compose
tags:
  - docker
  - m1

---
在 Mac M1的終端機，docker pull mysql image，出現如下的錯誤訊息：

  
<img decoding="async" src="https://i.imgur.com/h6wkxX3.png" alt="" /> 

<pre class="wp-block-code"><code class="">no matching manifest for linux/arm64/v8 in the manifest list entries</code></pre>



這個鏡像只有linux/amd64的架構，而M1是ARM芯片，所以pull下來的版本，沒有適用於arm64架構的mysql鏡像

到docker hub上看到的，也都是linux/amd64。  
<img decoding="async" src="https://i.imgur.com/DzDrdLN.png" alt="" /> 



從[docker的文檔][1]有說到：  
<img decoding="async" src="https://i.imgur.com/1sqm9qK.png" alt="" /> 



可以在終端機使用下方指令來

<pre class="wp-block-code"><code lang="docker" class="language-docker">docker pull --platform linux/amd64 mysql</code></pre>

<img decoding="async" src="https://i.imgur.com/MdIdaxw.png" alt="" />  
查看後安裝成功。

補充：  
如果是dockerfile，加上下面這行，就可以正常運行了：  
原本：

<pre class="wp-block-code"><code class="">FROM ubuntu:18.04</code></pre>

修改後：

<pre class="wp-block-code"><code class="">FROM --platform=linux/x86_64 ubuntu:18.04</code></pre>

 [1]: https://docs.docker.com/desktop/mac/apple-silicon/