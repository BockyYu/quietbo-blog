---
title: '[Virtualbox] 還原之前的備份與還原方式-快照 (必學)'
author: Bocky
type: post
date: 2021-07-03T18:30:15+00:00
url: /2021/07/04/virtualbox-還原之前的備份與還原方式-快照-必學/
categories:
  - virtualbox
tags:
  - virtualbox

---
最近工作又不小心把自己的環境弄壞了，用壞後有努力想要救回來，但就是被我搞到徹底的壞掉了，然後我還忘記做之前要快照，但還好有把某個時間點做快照，不至於整個系統要重灌。(如果要重灌使用一年的環境要很久…)

以下為操作版本:

<pre class="wp-block-code"><code class="">Virtualbox 6.1
ubuntu 20.04</code></pre>

快照功能簡述:  
可以保存虛擬機特定狀態，出現問題時想還原到正常狀態時，可以切換回以前的某狀態的快照。  
快照可以創建數多個，因此可以在虛擬機不同時間點的快照來回移動。  
VM運行時可以刪除快照，回收硬碟空間。

<div id="ez-toc-container" class="ez-toc-v2_0_82_2 ez-toc-wrap-center counter-hierarchy ez-toc-counter ez-toc-grey ez-toc-container-direction">
  <div class="ez-toc-title-container">
    <p class="ez-toc-title" style="cursor:inherit">
      Table of Contents
    </p>
    
    <span class="ez-toc-title-toggle"><a href="#" class="ez-toc-pull-right ez-toc-btn ez-toc-btn-xs ez-toc-btn-default ez-toc-toggle" aria-label="顯示/隱藏內容目錄"><span class="ez-toc-js-icon-con"><span class=""><span class="eztoc-hide" style="display:none;">Toggle</span><span class="ez-toc-icon-toggle-span"><svg style="fill: #999;color:#999" xmlns="http://www.w3.org/2000/svg" class="list-377408" width="20px" height="20px" viewBox="0 0 24 24" fill="none"><path d="M6 6H4v2h2V6zm14 0H8v2h12V6zM4 11h2v2H4v-2zm16 0H8v2h12v-2zM4 16h2v2H4v-2zm16 0H8v2h12v-2z" fill="currentColor"></path></svg><svg style="fill: #999;color:#999" class="arrow-unsorted-368013" xmlns="http://www.w3.org/2000/svg" width="10px" height="10px" viewBox="0 0 24 24" version="1.2" baseProfile="tiny"><path d="M18.2 9.3l-6.2-6.3-6.2 6.3c-.2.2-.3.4-.3.7s.1.5.3.7c.2.2.4.3.7.3h11c.3 0 .5-.1.7-.3.2-.2.3-.5.3-.7s-.1-.5-.3-.7zM5.8 14.7l6.2 6.3 6.2-6.3c.2-.2.3-.5.3-.7s-.1-.5-.3-.7c-.2-.2-.4-.3-.7-.3h-11c-.3 0-.5.1-.7.3-.2.2-.3.5-.3.7s.1.5.3.7z"/></svg></span></span></span></a></span>
  </div><nav>
  
  <ul class='ez-toc-list ez-toc-list-level-1 ' >
    <li class='ez-toc-page-1 ez-toc-heading-level-1'>
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2021/07/04/virtualbox-%e9%82%84%e5%8e%9f%e4%b9%8b%e5%89%8d%e7%9a%84%e5%82%99%e4%bb%bd%e8%88%87%e9%82%84%e5%8e%9f%e6%96%b9%e5%bc%8f-%e5%bf%ab%e7%85%a7-%e5%bf%85%e5%ad%b8/#%E8%A3%BD%E4%BD%9C%E5%BF%AB%E7%85%A7%E8%A3%BD%E4%BD%9C%E9%82%84%E5%8E%9F%E7%8B%80%E6%85%8B" >製作快照(製作還原狀態)</a><ul class='ez-toc-list-level-2' >
        <li class='ez-toc-heading-level-2'>
          <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2021/07/04/virtualbox-%e9%82%84%e5%8e%9f%e4%b9%8b%e5%89%8d%e7%9a%84%e5%82%99%e4%bb%bd%e8%88%87%e9%82%84%e5%8e%9f%e6%96%b9%e5%bc%8f-%e5%bf%ab%e7%85%a7-%e5%bf%85%e5%ad%b8/#%E6%96%B9%E6%B3%95%E4%B8%80" >方法一:</a>
        </li>
        <li class='ez-toc-page-1 ez-toc-heading-level-2'>
          <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2021/07/04/virtualbox-%e9%82%84%e5%8e%9f%e4%b9%8b%e5%89%8d%e7%9a%84%e5%82%99%e4%bb%bd%e8%88%87%e9%82%84%e5%8e%9f%e6%96%b9%e5%bc%8f-%e5%bf%ab%e7%85%a7-%e5%bf%85%e5%ad%b8/#%E6%96%B9%E6%B3%95%E4%BA%8C" >方法二:</a>
        </li>
      </ul>
    </li>
    
    <li class='ez-toc-page-1 ez-toc-heading-level-1'>
      <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2021/07/04/virtualbox-%e9%82%84%e5%8e%9f%e4%b9%8b%e5%89%8d%e7%9a%84%e5%82%99%e4%bb%bd%e8%88%87%e9%82%84%e5%8e%9f%e6%96%b9%e5%bc%8f-%e5%bf%ab%e7%85%a7-%e5%bf%85%e5%ad%b8/#%E9%82%84%E5%8E%9F" >還原</a>
    </li>
  </ul></nav>
</div>

# <span class="ez-toc-section" id="%E8%A3%BD%E4%BD%9C%E5%BF%AB%E7%85%A7%E8%A3%BD%E4%BD%9C%E9%82%84%E5%8E%9F%E7%8B%80%E6%85%8B"></span>製作快照(製作還原狀態)<span class="ez-toc-section-end"></span> 

## <span class="ez-toc-section" id="%E6%96%B9%E6%B3%95%E4%B8%80"></span>方法一:<span class="ez-toc-section-end"></span> 

開啟Virtualbox的快照畫面。  
<img decoding="async" src="https://i.imgur.com/3YVBpqh.png" alt="" />  
<img decoding="async" src="https://i.imgur.com/ZlSpZIQ.png" alt="" /> 

## <span class="ez-toc-section" id="%E6%96%B9%E6%B3%95%E4%BA%8C"></span>方法二:<span class="ez-toc-section-end"></span> 

方法二限於ubuntu開啟時: 機器 -> 取得快照  
<img decoding="async" src="https://i.imgur.com/3BSyHRP.png" alt="" /> 

一開始預設的名稱都是快照1  
建議命名時間日期，我是會照時間命名。  
<img decoding="async" src="https://i.imgur.com/oP7yWVt.png" alt="" /> 

點擊確認後稍等幾秒。  
<img decoding="async" src="https://i.imgur.com/B2JtEWR.png" alt="" /> 

開啟Virtualbox的快照畫面。  
<img decoding="async" src="https://i.imgur.com/3YVBpqh.png" alt="" /> 

紅框就是剛才做出來的快照。  
<img decoding="async" src="https://i.imgur.com/IpxjzCL.png" alt="" /> 

# <span class="ez-toc-section" id="%E9%82%84%E5%8E%9F"></span>還原<span class="ez-toc-section-end"></span> 

只要在ubuntu內的任意處增、刪、改檔案，然後正常關機。

Virtualbox的快照還原可以點擊，紅框快照就是備份的狀態，  
而藍框是做完快照後有做增、刪、改檔案的狀態。  
<img decoding="async" src="https://i.imgur.com/hGrLqo8.png" alt="" /> 

點擊還原後，會問要不要再建立&#8221;目前狀態&#8221;的快照，如果你不建立此時的快照，你所有狀態都會回到還原時的狀態，

意思就是問你要不要備份(快照)現在的狀態，不備份(快照)的話，以後想要回來現在的狀態就沒辦法囉!!!。  
<img decoding="async" src="https://i.imgur.com/qDhy7Ki.png" alt="" /> 

點擊還原後，一切都會回到當下快照的狀態。  
備份什麼時候的快照，就可以使用復原回到當下，只要你有做快照!

還原後就會變成下圖:  
<img decoding="async" src="https://i.imgur.com/uxumjsN.png" alt="" /> 

補充:  
檢視->取的螢幕快照。  
這裡的快照是螢幕截圖，跟本篇的快照無關。  
<img decoding="async" src="https://i.imgur.com/NhsGvDt.png" alt="" />