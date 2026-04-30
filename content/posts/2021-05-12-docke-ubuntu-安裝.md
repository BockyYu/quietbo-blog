---
title: '[Docke] ubuntu 安裝Docke'
author: Bocky
type: post
date: 2021-05-11T17:56:00+00:00
url: /2021/05/12/docke-ubuntu-安裝/
categories:
  - 'Docker&amp; Docker-compose'
tags:
  - docker
  - ubuntu
  - 安裝

---
以下為ubuntu20.04

<div id="ez-toc-container" class="ez-toc-v2_0_82_2 ez-toc-wrap-center counter-hierarchy ez-toc-counter ez-toc-grey ez-toc-container-direction">
  <div class="ez-toc-title-container">
    <p class="ez-toc-title" style="cursor:inherit">
      Table of Contents
    </p>
    
    <span class="ez-toc-title-toggle"><a href="#" class="ez-toc-pull-right ez-toc-btn ez-toc-btn-xs ez-toc-btn-default ez-toc-toggle" aria-label="顯示/隱藏內容目錄"><span class="ez-toc-js-icon-con"><span class=""><span class="eztoc-hide" style="display:none;">Toggle</span><span class="ez-toc-icon-toggle-span"><svg style="fill: #999;color:#999" xmlns="http://www.w3.org/2000/svg" class="list-377408" width="20px" height="20px" viewBox="0 0 24 24" fill="none"><path d="M6 6H4v2h2V6zm14 0H8v2h12V6zM4 11h2v2H4v-2zm16 0H8v2h12v-2zM4 16h2v2H4v-2zm16 0H8v2h12v-2z" fill="currentColor"></path></svg><svg style="fill: #999;color:#999" class="arrow-unsorted-368013" xmlns="http://www.w3.org/2000/svg" width="10px" height="10px" viewBox="0 0 24 24" version="1.2" baseProfile="tiny"><path d="M18.2 9.3l-6.2-6.3-6.2 6.3c-.2.2-.3.4-.3.7s.1.5.3.7c.2.2.4.3.7.3h11c.3 0 .5-.1.7-.3.2-.2.3-.5.3-.7s-.1-.5-.3-.7zM5.8 14.7l6.2 6.3 6.2-6.3c.2-.2.3-.5.3-.7s-.1-.5-.3-.7c-.2-.2-.4-.3-.7-.3h-11c-.3 0-.5.1-.7.3-.2.2-.3.5-.3.7s.1.5.3.7z"/></svg></span></span></span></a></span>
  </div><nav>
  
  <ul class='ez-toc-list ez-toc-list-level-1 ' >
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2021/05/12/docke-ubuntu-%e5%ae%89%e8%a3%9d/#Linux_%E5%AE%89%E8%A3%9Ddocker" >Linux 安裝docker</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2021/05/12/docke-ubuntu-%e5%ae%89%e8%a3%9d/#Linux_%E5%AE%89%E8%A3%9Ddocker_Compose" >Linux 安裝docker Compose</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2021/05/12/docke-ubuntu-%e5%ae%89%e8%a3%9d/#docker_%E5%88%87%E6%8F%9B%E4%BD%BF%E7%94%A8%E8%80%85" >docker 切換使用者</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2021/05/12/docke-ubuntu-%e5%ae%89%e8%a3%9d/#%E6%9B%B4%E6%96%B0apt%E5%8C%85%E8%B5%84%E6%BA%90%E7%B4%A2%E5%BC%95" >更新apt包资源索引</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-5" href="https://quietbo.com/2021/05/12/docke-ubuntu-%e5%ae%89%e8%a3%9d/#%E5%AE%89%E8%A3%9D%E8%BB%9F%E4%BB%B6%E5%8C%85%E4%BB%A5%E5%85%81%E8%A8%B1apt%E9%80%9A%E9%81%8EHTTPS%E4%BD%BF%E7%94%A8%E5%AD%98%E5%84%B2%E5%BA%AB" >安裝軟件包以允許apt通過HTTPS使用存儲庫:</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-6" href="https://quietbo.com/2021/05/12/docke-ubuntu-%e5%ae%89%e8%a3%9d/#%E9%87%8D%E6%96%B0%E9%96%8B%E5%95%9Fdocker" >重新開啟docker</a>
    </li>
  </ul></nav>
</div>

## <span class="ez-toc-section" id="Linux_%E5%AE%89%E8%A3%9Ddocker"></span>Linux 安裝docker<span class="ez-toc-section-end"></span> {.wp-block-heading}

在 Ubuntu Linux 中，使用 apt 安裝 Docker 比較方便：

<pre class="wp-block-code"><code lang="bash" class="language-bash">sudo apt-get install docker.io</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/6z0wwDO.png" alt="" /> </figure> 

安裝好之後，查看一下 docker 服務是否有正常啟動：

<pre class="wp-block-code"><code lang="bash" class="language-bash">service docker status</code></pre>

正常的話，應該可以看到綠色的狀態：  
<img decoding="async" src="https://i.imgur.com/UMvvP4N.png" alt="" /> 

<pre class="wp-block-code"><code lang="bash" class="language-bash">sudo usermod -aG docker 使用者名稱</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/SgP2HST.png" alt="" /> </figure> 

<pre class="wp-block-code"><code lang="bash" class="language-bash">docker version</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/QvrXKqq.png" alt="" /> </figure> <figure class="wp-block-image"><img decoding="async" src="https://i.imgur.com/B5QPKn6.png" alt="" /></figure> 

## <span class="ez-toc-section" id="Linux_%E5%AE%89%E8%A3%9Ddocker_Compose"></span>Linux 安裝docker Compose<span class="ez-toc-section-end"></span> {.wp-block-heading}

<pre class="wp-block-code"><code lang="bash" class="language-bash">sudo curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose</code></pre>

<pre class="wp-block-code"><code lang="bash" class="language-bash">sudo gpasswd -a ${USER} docker</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/L9WTE0i.png" alt="" /> </figure> 

## <span class="ez-toc-section" id="docker_%E5%88%87%E6%8F%9B%E4%BD%BF%E7%94%A8%E8%80%85"></span>docker 切換使用者<span class="ez-toc-section-end"></span> {.wp-block-heading}

<ol class="wp-block-list">
  <li>
    將使用者加入群組
  </li>
</ol>

<pre class="wp-block-code"><code class="">sudo gpasswd -a ${USER} docker</code></pre>

<ol class="wp-block-list" start="2">
  <li>
    切換到超級使用者
  </li>
</ol>

<pre class="wp-block-code"><code class="">sudo su</code></pre>

<ol class="wp-block-list" start="3">
  <li>
    切回使用者
  </li>
</ol>

<pre class="wp-block-code"><code class="">su ubuntu</code></pre>

## <span class="ez-toc-section" id="%E6%9B%B4%E6%96%B0apt%E5%8C%85%E8%B5%84%E6%BA%90%E7%B4%A2%E5%BC%95"></span>更新apt包资源索引<span class="ez-toc-section-end"></span> {.wp-block-heading}

<pre class="wp-block-code"><code class="">sudo apt-get update</code></pre>

## <span class="ez-toc-section" id="%E5%AE%89%E8%A3%9D%E8%BB%9F%E4%BB%B6%E5%8C%85%E4%BB%A5%E5%85%81%E8%A8%B1apt%E9%80%9A%E9%81%8EHTTPS%E4%BD%BF%E7%94%A8%E5%AD%98%E5%84%B2%E5%BA%AB"></span>安裝軟件包以允許apt通過HTTPS使用存儲庫:<span class="ez-toc-section-end"></span> {.wp-block-heading}

<pre class="wp-block-code"><code class="">sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common</code></pre>



## <span class="ez-toc-section" id="%E9%87%8D%E6%96%B0%E9%96%8B%E5%95%9Fdocker"></span>重新開啟docker<span class="ez-toc-section-end"></span> {.wp-block-heading}

  
有次早上要執行docker-compose的時候無法正常開啟，出現下方錯誤訊息

<pre class="wp-block-code"><code lang="bash" class="language-bash">ERROR: Couldn't connect to Docker daemon at http+docker://localhost - is it running?

If it's at a non-standard location, specify the URL with the DOCKER_HOST environment variable.</code></pre>

當時已經設好群組卻還是一樣，所以有可能就是docker不知道原因**<span style="text-decoration: underline;">被關閉</span>**了。  
下方指令為重新開啟docker的方式。

<pre class="wp-block-code"><code lang="docker" class="language-docker line-numbers">service docker start
sudo docker-compose up</code></pre>