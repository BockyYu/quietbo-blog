---
title: '[Python] 與MongoDB連接(並使用GUI:Studio 3T)'
author: Bocky
type: post
date: 2023-01-09T15:13:00+00:00
url: /2023/01/09/python-與mongodb連接並使用guistudio-3t/
categories:
  - Editor;IDE;GUI
  - 程式語言
  - 系統相關
tags:
  - Studio 3T

---
本篇使用虛擬機VMware安裝ubuntu20.04，並安裝docker。  
Windows使用GUI [Studio 3T][1]

請自行先安裝VMware、ubuntu、docker及Studio 3T。

<div id="ez-toc-container" class="ez-toc-v2_0_82_2 ez-toc-wrap-center counter-hierarchy ez-toc-counter ez-toc-grey ez-toc-container-direction">
  <div class="ez-toc-title-container">
    <p class="ez-toc-title" style="cursor:inherit">
      Table of Contents
    </p>
    
    <span class="ez-toc-title-toggle"><a href="#" class="ez-toc-pull-right ez-toc-btn ez-toc-btn-xs ez-toc-btn-default ez-toc-toggle" aria-label="顯示/隱藏內容目錄"><span class="ez-toc-js-icon-con"><span class=""><span class="eztoc-hide" style="display:none;">Toggle</span><span class="ez-toc-icon-toggle-span"><svg style="fill: #999;color:#999" xmlns="http://www.w3.org/2000/svg" class="list-377408" width="20px" height="20px" viewBox="0 0 24 24" fill="none"><path d="M6 6H4v2h2V6zm14 0H8v2h12V6zM4 11h2v2H4v-2zm16 0H8v2h12v-2zM4 16h2v2H4v-2zm16 0H8v2h12v-2z" fill="currentColor"></path></svg><svg style="fill: #999;color:#999" class="arrow-unsorted-368013" xmlns="http://www.w3.org/2000/svg" width="10px" height="10px" viewBox="0 0 24 24" version="1.2" baseProfile="tiny"><path d="M18.2 9.3l-6.2-6.3-6.2 6.3c-.2.2-.3.4-.3.7s.1.5.3.7c.2.2.4.3.7.3h11c.3 0 .5-.1.7-.3.2-.2.3-.5.3-.7s-.1-.5-.3-.7zM5.8 14.7l6.2 6.3 6.2-6.3c.2-.2.3-.5.3-.7s-.1-.5-.3-.7c-.2-.2-.4-.3-.7-.3h-11c-.3 0-.5.1-.7.3-.2.2-.3.5-.3.7s.1.5.3.7z"/></svg></span></span></span></a></span>
  </div><nav>
  
  <ul class='ez-toc-list ez-toc-list-level-1 ' >
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2023/01/09/python-%e8%88%87mongodb%e9%80%a3%e6%8e%a5%e4%b8%a6%e4%bd%bf%e7%94%a8guistudio-3t/#ubuntu%E5%AE%89%E8%A3%9Ddocker_mongodb" >ubuntu安裝docker mongodb</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2023/01/09/python-%e8%88%87mongodb%e9%80%a3%e6%8e%a5%e4%b8%a6%e4%bd%bf%e7%94%a8guistudio-3t/#%E6%9F%A5%E8%A9%A2%E8%A9%B2ubuntu%E7%9A%84IP%E4%BD%8D%E5%9D%80" >查詢該ubuntu的IP位址</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2023/01/09/python-%e8%88%87mongodb%e9%80%a3%e6%8e%a5%e4%b8%a6%e4%bd%bf%e7%94%a8guistudio-3t/#Windows%E5%AE%89%E8%A3%9DStudio_3T" >Windows安裝Studio 3T</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2023/01/09/python-%e8%88%87mongodb%e9%80%a3%e6%8e%a5%e4%b8%a6%e4%bd%bf%e7%94%a8guistudio-3t/#%E5%A6%82%E4%BD%95%E9%80%B2%E5%85%A5docker%E5%85%A7%E7%9A%84mongodb" >如何進入docker內的mongodb?</a>
    </li>
  </ul></nav>
</div>

## <span class="ez-toc-section" id="ubuntu%E5%AE%89%E8%A3%9Ddocker_mongodb"></span>ubuntu安裝docker mongodb<span class="ez-toc-section-end"></span> {.wp-block-heading}

下載image

<pre class="wp-block-code"><code lang="docker" class="language-docker">docker pull mongo:latest</code></pre>

啟動容器

<pre class="wp-block-code"><code lang="docker" class="language-docker">docker run --name mongo -v /d/tmp/mongo/data:/data/db -d -p 27017:27017 mongo:latest</code></pre>

<ul class="wp-block-list">
  <li>
    &#8211;name 指定建起來的container名字
  </li>
  <li>
    -v 連結local端目錄與container目錄 (像Linux中mount共用空間的概念)
  </li>
  <li>
    -d 背景執行
  </li>
  <li>
    -p 指定將docker內的27017 port 與本地端(ubuntu)的27017 port連結在一起，這樣就可以透過本地直接連container了
  </li>
</ul>

若ubuntu重新啟動發現容器沒有up是正常的，只要在重新使用start就可以起來了，

<pre class="wp-block-code"><code class="">docker ps -a
docker start {CONTAINER_ID}</code></pre>

範例:docker start 242c45f0ab65  
up正常為下圖:  
<img decoding="async" src="https://i.imgur.com/2loo39c.png" alt="" /> 

## <span class="ez-toc-section" id="%E6%9F%A5%E8%A9%A2%E8%A9%B2ubuntu%E7%9A%84IP%E4%BD%8D%E5%9D%80"></span>查詢該ubuntu的IP位址<span class="ez-toc-section-end"></span> {.wp-block-heading}

右上角網路資訊點進去到這頁面會看到ubnutu的ip  
<img decoding="async" src="https://i.imgur.com/mtAd6ZL.png" alt="" /> 

## <span class="ez-toc-section" id="Windows%E5%AE%89%E8%A3%9DStudio_3T"></span>Windows安裝Studio 3T<span class="ez-toc-section-end"></span> {.wp-block-heading}

GUI [Studio 3T][1]

設置與ubuntu內的mongodb

點Connect建立New Connect。  
<img decoding="async" src="https://i.imgur.com/Uz82ZC5.png" alt="" />  
<img decoding="async" src="https://i.imgur.com/xSPR4yk.png" alt="" /> 

成功會出現下圖  
<img decoding="async" src="https://i.imgur.com/oAkMC9W.png" alt="" /> 

## <span class="ez-toc-section" id="%E5%A6%82%E4%BD%95%E9%80%B2%E5%85%A5docker%E5%85%A7%E7%9A%84mongodb"></span>如何進入docker內的mongodb?<span class="ez-toc-section-end"></span> {.wp-block-heading}

<ol class="wp-block-list">
  <li>
    進入容器，指令:docker exec -it 容器ID bash
  </li>
  <li>
    進入容器後輸入:mongosh
  </li>
</ol>

下圖為成功進入docker內的mongodb  
<img decoding="async" src="https://i.imgur.com/JKKB3re.png" alt="" /> 



補充  
如果沒連上可能是ubuntu 27017的port沒有分享出來。

 [1]: https://studio3t.com/