---
title: '[Pycharm] 退出 run pytest'
author: Bocky
type: post
date: 2021-06-11T09:11:30+00:00
url: /2021/06/11/pycharm-退出-run-pytest/
categories:
  - Editor;IDE;GUI
tags:
  - pycharm

---
某次安裝pytest後，在執行程式都會自動用pytest，但我其實很少用到pytest，可又不想把Package刪除。

<div id="ez-toc-container" class="ez-toc-v2_0_82_2 ez-toc-wrap-center counter-hierarchy ez-toc-counter ez-toc-grey ez-toc-container-direction">
  <div class="ez-toc-title-container">
    <p class="ez-toc-title" style="cursor:inherit">
      Table of Contents
    </p>
    
    <span class="ez-toc-title-toggle"><a href="#" class="ez-toc-pull-right ez-toc-btn ez-toc-btn-xs ez-toc-btn-default ez-toc-toggle" aria-label="顯示/隱藏內容目錄"><span class="ez-toc-js-icon-con"><span class=""><span class="eztoc-hide" style="display:none;">Toggle</span><span class="ez-toc-icon-toggle-span"><svg style="fill: #999;color:#999" xmlns="http://www.w3.org/2000/svg" class="list-377408" width="20px" height="20px" viewBox="0 0 24 24" fill="none"><path d="M6 6H4v2h2V6zm14 0H8v2h12V6zM4 11h2v2H4v-2zm16 0H8v2h12v-2zM4 16h2v2H4v-2zm16 0H8v2h12v-2z" fill="currentColor"></path></svg><svg style="fill: #999;color:#999" class="arrow-unsorted-368013" xmlns="http://www.w3.org/2000/svg" width="10px" height="10px" viewBox="0 0 24 24" version="1.2" baseProfile="tiny"><path d="M18.2 9.3l-6.2-6.3-6.2 6.3c-.2.2-.3.4-.3.7s.1.5.3.7c.2.2.4.3.7.3h11c.3 0 .5-.1.7-.3.2-.2.3-.5.3-.7s-.1-.5-.3-.7zM5.8 14.7l6.2 6.3 6.2-6.3c.2-.2.3-.5.3-.7s-.1-.5-.3-.7c-.2-.2-.4-.3-.7-.3h-11c-.3 0-.5.1-.7.3-.2.2-.3.5-.3.7s.1.5.3.7z"/></svg></span></span></span></a></span>
  </div><nav>
  
  <ul class='ez-toc-list ez-toc-list-level-1 ' >
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2021/06/11/pycharm-%e9%80%80%e5%87%ba-run-pytest/#%E5%A6%82%E4%BD%95%E6%AA%A2%E6%9F%A5%E6%98%AF%E5%90%A6%E5%B7%B2%E5%AE%89%E8%A3%9Dpytest%E7%9A%84package" >如何檢查是否已安裝pytest的package?</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2021/06/11/pycharm-%e9%80%80%e5%87%ba-run-pytest/#%E6%96%B9%E6%B3%951%E7%9F%AD%E6%9C%9F%E8%A7%A3%E6%B1%BA%E5%95%8F%E9%A1%8C%E7%94%A8" >方法1(短期解決問題用):</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2021/06/11/pycharm-%e9%80%80%e5%87%ba-run-pytest/#%E6%96%B9%E6%B3%952" >方法2:</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2021/06/11/pycharm-%e9%80%80%e5%87%ba-run-pytest/#%E6%96%B9%E6%B3%953" >方法3:</a>
    </li>
  </ul></nav>
</div>

## <span class="ez-toc-section" id="%E5%A6%82%E4%BD%95%E6%AA%A2%E6%9F%A5%E6%98%AF%E5%90%A6%E5%B7%B2%E5%AE%89%E8%A3%9Dpytest%E7%9A%84package"></span>如何檢查是否已安裝pytest的package?<span class="ez-toc-section-end"></span> {.wp-block-heading}

File -> settings -> Project:xxxx -> Project Interpreter<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/XQSdgQp.png" alt="" /> </figure> 

如果需要移除，就點右方的&#8221;-&#8220;

## <span class="ez-toc-section" id="%E6%96%B9%E6%B3%951%E7%9F%AD%E6%9C%9F%E8%A7%A3%E6%B1%BA%E5%95%8F%E9%A1%8C%E7%94%A8"></span>方法1(短期解決問題用):<span class="ez-toc-section-end"></span> {.wp-block-heading}

指定一般執行模式上方run -> Run…

<pre class="wp-block-code"><code class="">如果點Run 'pytest in XXXXX.py'，又會在執行pytest。</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/ig2F7pt.png" alt="" /> </figure> <figure class="wp-block-image"><img decoding="async" src="https://i.imgur.com/KhiWAZs.png" alt="" /></figure> 

## <span class="ez-toc-section" id="%E6%96%B9%E6%B3%952"></span>方法2:<span class="ez-toc-section-end"></span> {.wp-block-heading}<figure class="wp-block-image is-resized">

<img loading="lazy" decoding="async" src="https://i.imgur.com/ig2F7pt.png" alt="" width="804" height="88" /> </figure> <figure class="wp-block-image"><img decoding="async" src="https://i.imgur.com/j1qkHAa.png" alt="" /></figure> 

將Python test內想去掉的文件點選後點擊上面的&#8217;-&#8216;號。  
<img decoding="async" src="https://i.imgur.com/X2dw0WI.png" alt="" /> 

## <span class="ez-toc-section" id="%E6%96%B9%E6%B3%953"></span>方法3:<span class="ez-toc-section-end"></span> {.wp-block-heading}

File -> settings -> Tools -> Python Integrated Tools

查看Default test runner ，如果現在是pytest，則改成Unittests  
<img decoding="async" src="https://i.imgur.com/idxFJNb.png" alt="" /> 

之後要寫C#改用VSCode了，短時間應該不會有Pycharm的文章。