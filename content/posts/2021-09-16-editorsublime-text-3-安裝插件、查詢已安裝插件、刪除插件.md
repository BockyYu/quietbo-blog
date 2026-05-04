---
title: '[Editor]Sublime Text 3 安裝插件、查詢已安裝插件、刪除插件'
author: Bocky
type: post
date: 2021-09-16T11:26:08+00:00
url: /2021/09/16/editorsublime-text-3-安裝插件、查詢已安裝插件、刪除插件/
categories:
  - Editor;IDE;GUI
tags:
  - sublime

---
<div id="ez-toc-container" class="ez-toc-v2_0_82_2 ez-toc-wrap-center counter-hierarchy ez-toc-counter ez-toc-grey ez-toc-container-direction">
  <div class="ez-toc-title-container">
    <p class="ez-toc-title" style="cursor:inherit">
      Table of Contents
    </p>
    
    <span class="ez-toc-title-toggle"><a href="#" class="ez-toc-pull-right ez-toc-btn ez-toc-btn-xs ez-toc-btn-default ez-toc-toggle" aria-label="顯示/隱藏內容目錄"><span class="ez-toc-js-icon-con"><span class=""><span class="eztoc-hide" style="display:none;">Toggle</span><span class="ez-toc-icon-toggle-span"><svg style="fill: #999;color:#999" xmlns="http://www.w3.org/2000/svg" class="list-377408" width="20px" height="20px" viewBox="0 0 24 24" fill="none"><path d="M6 6H4v2h2V6zm14 0H8v2h12V6zM4 11h2v2H4v-2zm16 0H8v2h12v-2zM4 16h2v2H4v-2zm16 0H8v2h12v-2z" fill="currentColor"></path></svg><svg style="fill: #999;color:#999" class="arrow-unsorted-368013" xmlns="http://www.w3.org/2000/svg" width="10px" height="10px" viewBox="0 0 24 24" version="1.2" baseProfile="tiny"><path d="M18.2 9.3l-6.2-6.3-6.2 6.3c-.2.2-.3.4-.3.7s.1.5.3.7c.2.2.4.3.7.3h11c.3 0 .5-.1.7-.3.2-.2.3-.5.3-.7s-.1-.5-.3-.7zM5.8 14.7l6.2 6.3 6.2-6.3c.2-.2.3-.5.3-.7s-.1-.5-.3-.7c-.2-.2-.4-.3-.7-.3h-11c-.3 0-.5.1-.7.3-.2.2-.3.5-.3.7s.1.5.3.7z"/></svg></span></span></span></a></span>
  </div><nav>
  
  <ul class='ez-toc-list ez-toc-list-level-1 ' >
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2021/09/16/editorsublime-text-3-%e5%ae%89%e8%a3%9d%e6%8f%92%e4%bb%b6%e3%80%81%e6%9f%a5%e8%a9%a2%e5%b7%b2%e5%ae%89%e8%a3%9d%e6%8f%92%e4%bb%b6%e3%80%81%e5%88%aa%e9%99%a4%e6%8f%92%e4%bb%b6/#%E5%AE%89%E8%A3%9D%E6%8F%92%E4%BB%B6" >安裝插件</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2021/09/16/editorsublime-text-3-%e5%ae%89%e8%a3%9d%e6%8f%92%e4%bb%b6%e3%80%81%e6%9f%a5%e8%a9%a2%e5%b7%b2%e5%ae%89%e8%a3%9d%e6%8f%92%e4%bb%b6%e3%80%81%e5%88%aa%e9%99%a4%e6%8f%92%e4%bb%b6/#%E6%9F%A5%E8%A9%A2%E5%B7%B2%E5%AE%89%E8%A3%9D%E6%8F%92%E4%BB%B6" >查詢已安裝插件</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2021/09/16/editorsublime-text-3-%e5%ae%89%e8%a3%9d%e6%8f%92%e4%bb%b6%e3%80%81%e6%9f%a5%e8%a9%a2%e5%b7%b2%e5%ae%89%e8%a3%9d%e6%8f%92%e4%bb%b6%e3%80%81%e5%88%aa%e9%99%a4%e6%8f%92%e4%bb%b6/#%E6%9B%B4%E6%96%B0%E6%8F%92%E4%BB%B6" >更新插件</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2021/09/16/editorsublime-text-3-%e5%ae%89%e8%a3%9d%e6%8f%92%e4%bb%b6%e3%80%81%e6%9f%a5%e8%a9%a2%e5%b7%b2%e5%ae%89%e8%a3%9d%e6%8f%92%e4%bb%b6%e3%80%81%e5%88%aa%e9%99%a4%e6%8f%92%e4%bb%b6/#%E5%88%AA%E9%99%A4%E6%8F%92%E4%BB%B6" >刪除插件</a>
    </li>
  </ul></nav>
</div>

## <span class="ez-toc-section" id="%E5%AE%89%E8%A3%9D%E6%8F%92%E4%BB%B6"></span>安裝插件<span class="ez-toc-section-end"></span> 

<ol class="wp-block-list">
  <li>
    ctrl + shift + P，輸入&#8221;Package Control&#8221;
  </li>
  <li>
    點擊 Package Control:install Package<br /><img decoding="async" src="https://i.imgur.com/RB7LtVL.png" alt="" />
  </li>
  <li>
    輸入要安裝的package名稱，下面會跳出相似的package名稱，再選擇自己要的即可<br /><img decoding="async" src="https://i.imgur.com/4awRV9j.png" alt="" />
  </li>
</ol>

## <span class="ez-toc-section" id="%E6%9F%A5%E8%A9%A2%E5%B7%B2%E5%AE%89%E8%A3%9D%E6%8F%92%E4%BB%B6"></span>查詢已安裝插件<span class="ez-toc-section-end"></span> 

步骤如下:

<ol class="wp-block-list">
  <li>
    ctrl + shift + P，輸入&#8221;Package Control&#8221;
  </li>
  <li>
    點擊Package Control：List Packages<br /><img decoding="async" src="https://i.imgur.com/U3XBPYF.png" alt="" />
  </li>
  <li>
    查看已安装插件列表(下圖為範例)<br />以列表的形式顯示，可通過鍵盤上下鍵或者滑鼠滾輪來查看列表。<br /><img decoding="async" src="https://i.imgur.com/4sQsqyD.png" alt="" />
  </li>
</ol>

## <span class="ez-toc-section" id="%E6%9B%B4%E6%96%B0%E6%8F%92%E4%BB%B6"></span>更新插件<span class="ez-toc-section-end"></span> 

<ol class="wp-block-list">
  <li>
    ctrl + shift + P，輸入 upgrade packages後按下Enter。
  </li>
  <li>
    如果有可更新的插件，下方會顯示(但這次沒有可更新的插件，無法提供圖片)<br /><img decoding="async" src="https://i.imgur.com/oeCrmks.png" alt="" />
  </li>
</ol>

## <span class="ez-toc-section" id="%E5%88%AA%E9%99%A4%E6%8F%92%E4%BB%B6"></span>刪除插件<span class="ez-toc-section-end"></span> 

<ol class="wp-block-list">
  <li>
    ctrl + shift + P，輸入&#8221;Package Control&#8221;
  </li>
  <li>
    選擇Package Control:remove package<br /><img decoding="async" src="https://i.imgur.com/HLv4XWX.png" alt="" />
  </li>
  <li>
    選擇要刪除的package<br /><img decoding="async" src="https://i.imgur.com/NovqD6r.png" alt="" />
  </li>
</ol>