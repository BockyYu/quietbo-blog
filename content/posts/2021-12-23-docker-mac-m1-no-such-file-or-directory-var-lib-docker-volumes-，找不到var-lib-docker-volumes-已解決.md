---
title: '[Docker] Mac M1 – no such file or directory: /var/lib/docker/volumes ，找不到var/lib/docker/volumes (已解決)'
author: Bocky
type: post
date: 2021-12-22T17:29:36+00:00
url: /2021/12/23/docker-mac-m1-no-such-file-or-directory-var-lib-docker-volumes-，找不到var-lib-docker-volumes-已解決/
categories:
  - 'Docker&amp; Docker-compose'
tags:
  - docker
  - mac

---
<ul class="wp-block-list">
  <li>
    Mac M1 version 12.0.1
  </li>
  <li>
    Docker version 20.10.11
  </li>
</ul><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/porV5EQ.png" alt="" /> </figure> 

嘗試進入這個路徑時，發現它並不存在<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/64ZyrW9.png" alt="" /> </figure> 

網路上有許多解決方式是使用下方指令，但仍錯誤。

<pre class="wp-block-code"><code class="">screen ~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/tty</code></pre>

嘗試之後直接閃退：

<pre class="wp-block-code"><code class="">[screen is terminating]</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/ghCOFSw.png" alt="" /> </figure> 

<div id="ez-toc-container" class="ez-toc-v2_0_82_2 ez-toc-wrap-center counter-hierarchy ez-toc-counter ez-toc-grey ez-toc-container-direction">
  <div class="ez-toc-title-container">
    <p class="ez-toc-title" style="cursor:inherit">
      Table of Contents
    </p>
    
    <span class="ez-toc-title-toggle"><a href="#" class="ez-toc-pull-right ez-toc-btn ez-toc-btn-xs ez-toc-btn-default ez-toc-toggle" aria-label="顯示/隱藏內容目錄"><span class="ez-toc-js-icon-con"><span class=""><span class="eztoc-hide" style="display:none;">Toggle</span><span class="ez-toc-icon-toggle-span"><svg style="fill: #999;color:#999" xmlns="http://www.w3.org/2000/svg" class="list-377408" width="20px" height="20px" viewBox="0 0 24 24" fill="none"><path d="M6 6H4v2h2V6zm14 0H8v2h12V6zM4 11h2v2H4v-2zm16 0H8v2h12v-2zM4 16h2v2H4v-2zm16 0H8v2h12v-2z" fill="currentColor"></path></svg><svg style="fill: #999;color:#999" class="arrow-unsorted-368013" xmlns="http://www.w3.org/2000/svg" width="10px" height="10px" viewBox="0 0 24 24" version="1.2" baseProfile="tiny"><path d="M18.2 9.3l-6.2-6.3-6.2 6.3c-.2.2-.3.4-.3.7s.1.5.3.7c.2.2.4.3.7.3h11c.3 0 .5-.1.7-.3.2-.2.3-.5.3-.7s-.1-.5-.3-.7zM5.8 14.7l6.2 6.3 6.2-6.3c.2-.2.3-.5.3-.7s-.1-.5-.3-.7c-.2-.2-.4-.3-.7-.3h-11c-.3 0-.5.1-.7.3-.2.2-.3.5-.3.7s.1.5.3.7z"/></svg></span></span></span></a></span>
  </div><nav>
  
  <ul class='ez-toc-list ez-toc-list-level-1 ' >
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2021/12/23/docker-mac-m1-no-such-file-or-directory-var-lib-docker-volumes-%ef%bc%8c%e6%89%be%e4%b8%8d%e5%88%b0var-lib-docker-volumes-%e5%b7%b2%e8%a7%a3%e6%b1%ba/#1%E8%A7%A3%E6%B1%BA%E9%96%83%E9%80%80%E5%95%8F%E9%A1%8C%E6%96%B9%E5%BC%8F" >1.解決閃退問題方式</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2021/12/23/docker-mac-m1-no-such-file-or-directory-var-lib-docker-volumes-%ef%bc%8c%e6%89%be%e4%b8%8d%e5%88%b0var-lib-docker-volumes-%e5%b7%b2%e8%a7%a3%e6%b1%ba/#2%E6%AA%A2%E8%A6%96volumes" >2.檢視volumes</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2021/12/23/docker-mac-m1-no-such-file-or-directory-var-lib-docker-volumes-%ef%bc%8c%e6%89%be%e4%b8%8d%e5%88%b0var-lib-docker-volumes-%e5%b7%b2%e8%a7%a3%e6%b1%ba/#%E8%A3%9C%E5%85%85%EF%BC%9A" >補充：</a><ul class='ez-toc-list-level-3' >
        <li class='ez-toc-heading-level-3'>
          <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2021/12/23/docker-mac-m1-no-such-file-or-directory-var-lib-docker-volumes-%ef%bc%8c%e6%89%be%e4%b8%8d%e5%88%b0var-lib-docker-volumes-%e5%b7%b2%e8%a7%a3%e6%b1%ba/#%E9%80%B2%E5%85%A5Mountpoint%E5%B0%8D%E6%87%89%E7%9A%84%E8%B3%87%E6%96%99%E5%A4%BE_Linux" >進入Mountpoint對應的資料夾 (Linux)</a>
        </li>
      </ul>
    </li>
  </ul></nav>
</div>

## <span class="ez-toc-section" id="1%E8%A7%A3%E6%B1%BA%E9%96%83%E9%80%80%E5%95%8F%E9%A1%8C%E6%96%B9%E5%BC%8F"></span>1.解決閃退問題方式<span class="ez-toc-section-end"></span> 

詳細可參考此篇：[Where is /var/lib/docker on Mac/OS X][1]  
mac下docker實際是在vm裡又加了一層，因此需要進入vm 才能進行操作。

<ul class="wp-block-list">
  <li>
    終端機執行下方指令
  </li>
</ul>

<pre class="wp-block-code"><code class="">docker run -it --privileged --pid=host debian nsenter -t 1 -m -u -n -i sh</code></pre>

## <span class="ez-toc-section" id="2%E6%AA%A2%E8%A6%96volumes"></span>2.檢視volumes<span class="ez-toc-section-end"></span> 

解決閃退問題後，會進入VM內，輸入ls，檢視當前路徑下目錄資訊。

<pre class="wp-block-code"><code class="">ls /var/lib/docker/volumes/</code></pre>

找到我要的mysql-data，而其他卷掛載都在這個目錄下：  
<img decoding="async" src="https://i.imgur.com/6LVBW4n.png" alt="" /> 

退出：exit



## <span class="ez-toc-section" id="%E8%A3%9C%E5%85%85%EF%BC%9A"></span>補充：<span class="ez-toc-section-end"></span> 

### <span class="ez-toc-section" id="%E9%80%B2%E5%85%A5Mountpoint%E5%B0%8D%E6%87%89%E7%9A%84%E8%B3%87%E6%96%99%E5%A4%BE_Linux"></span>進入Mountpoint對應的資料夾 (Linux)<span class="ez-toc-section-end"></span> 

如果使用Linux，可以直接找到Mountpoint對應的目錄，就是和container連接的地方，這裡面的改動和container內是同步的。  
但如果是Mac，用同樣的方式想要進入Mountpoint對應的目錄，會不存在，

Mac需要先創建一個Linux的VM，所以Mountpoint對應的不是Mac裡可以找得到的檔案，而是要到那個VM裡去找，

 [1]: https://stackoverflow.com/questions/38532483/where-is-var-lib-docker-on-mac-os-x/65645462#65645462