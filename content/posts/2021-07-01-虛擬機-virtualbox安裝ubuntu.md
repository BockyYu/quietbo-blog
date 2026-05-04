---
title: '[Virtualbox] 安裝ubuntu20.04'
author: Bocky
type: post
date: 2021-07-01T12:00:25+00:00
url: /2021/07/01/虛擬機-virtualbox安裝ubuntu/
categories:
  - virtualbox
tags:
  - virtualbox
  - 安裝

---
工作配Windows但開發時都用Linux，然後自己就很常弄壞環境，菜雞時期都是建新的，常用的工具在慢慢裝回來，後來學會備份(映像檔)和快照後，弄壞弄的更安心了呢(?)，但還是菜，bug(菜蟲)都掉滿地了。  
真心建議安裝完後可以去學個【<a rel="noreferrer noopener" href="https://quietbo.com/2021/07/04/virtualbox-%e9%82%84%e5%8e%9f%e4%b9%8b%e5%89%8d%e7%9a%84%e5%82%99%e4%bb%bd%e8%88%87%e9%82%84%e5%8e%9f%e6%96%b9%e5%bc%8f-%e5%bf%ab%e7%85%a7-%e5%bf%85%e5%ad%b8/?preview=true" target="_blank">Virtualbox 快照</a>】、 【 <a href="https://quietbo.com/2021/08/12/virtualbox-%e7%b3%bb%e7%b5%b1%e5%82%99%e4%bb%bd%e6%98%a0%e8%b1%a1%e6%aa%94/" data-type="URL" data-id="https://quietbo.com/2021/08/12/virtualbox-%e7%b3%bb%e7%b5%b1%e5%82%99%e4%bb%bd%e6%98%a0%e8%b1%a1%e6%aa%94/">系統備份映象檔</a>】 功能，也許哪天環境有問題，怎麼辦都解決不了的時候，快照也許能幫上忙，至少不用全部都重新安裝。

<div id="ez-toc-container" class="ez-toc-v2_0_82_2 ez-toc-wrap-center counter-hierarchy ez-toc-counter ez-toc-grey ez-toc-container-direction">
  <div class="ez-toc-title-container">
    <p class="ez-toc-title" style="cursor:inherit">
      Table of Contents
    </p>
    
    <span class="ez-toc-title-toggle"><a href="#" class="ez-toc-pull-right ez-toc-btn ez-toc-btn-xs ez-toc-btn-default ez-toc-toggle" aria-label="顯示/隱藏內容目錄"><span class="ez-toc-js-icon-con"><span class=""><span class="eztoc-hide" style="display:none;">Toggle</span><span class="ez-toc-icon-toggle-span"><svg style="fill: #999;color:#999" xmlns="http://www.w3.org/2000/svg" class="list-377408" width="20px" height="20px" viewBox="0 0 24 24" fill="none"><path d="M6 6H4v2h2V6zm14 0H8v2h12V6zM4 11h2v2H4v-2zm16 0H8v2h12v-2zM4 16h2v2H4v-2zm16 0H8v2h12v-2z" fill="currentColor"></path></svg><svg style="fill: #999;color:#999" class="arrow-unsorted-368013" xmlns="http://www.w3.org/2000/svg" width="10px" height="10px" viewBox="0 0 24 24" version="1.2" baseProfile="tiny"><path d="M18.2 9.3l-6.2-6.3-6.2 6.3c-.2.2-.3.4-.3.7s.1.5.3.7c.2.2.4.3.7.3h11c.3 0 .5-.1.7-.3.2-.2.3-.5.3-.7s-.1-.5-.3-.7zM5.8 14.7l6.2 6.3 6.2-6.3c.2-.2.3-.5.3-.7s-.1-.5-.3-.7c-.2-.2-.4-.3-.7-.3h-11c-.3 0-.5.1-.7.3-.2.2-.3.5-.3.7s.1.5.3.7z"/></svg></span></span></span></a></span>
  </div><nav>
  
  <ul class='ez-toc-list ez-toc-list-level-1 ' >
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2021/07/01/%e8%99%9b%e6%93%ac%e6%a9%9f-virtualbox%e5%ae%89%e8%a3%9dubuntu/#%E5%AE%89%E8%A3%9D" >安裝</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2021/07/01/%e8%99%9b%e6%93%ac%e6%a9%9f-virtualbox%e5%ae%89%e8%a3%9dubuntu/#%E8%A7%A3%E6%9E%90%E5%BA%A6%E8%A8%AD%E5%AE%9A" >解析度設定</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2021/07/01/%e8%99%9b%e6%93%ac%e6%a9%9f-virtualbox%e5%ae%89%e8%a3%9dubuntu/#%E8%A8%AD%E5%AE%9A%E5%8F%AF%E4%BB%A5%E9%9B%99%E5%90%91%E5%89%AA%E8%B2%BC" >設定可以雙向剪貼</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2021/07/01/%e8%99%9b%e6%93%ac%e6%a9%9f-virtualbox%e5%ae%89%e8%a3%9dubuntu/#%E5%85%B1%E4%BA%AB%E8%B3%87%E6%96%99%E5%A4%BE" >共享資料夾</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-5" href="https://quietbo.com/2021/07/01/%e8%99%9b%e6%93%ac%e6%a9%9f-virtualbox%e5%ae%89%e8%a3%9dubuntu/#%E7%95%AB%E9%9D%A2%E5%A4%A7%E5%B0%8F" >畫面大小</a>
    </li>
  </ul></nav>
</div>

## <span class="ez-toc-section" id="%E5%AE%89%E8%A3%9D"></span>安裝<span class="ez-toc-section-end"></span> 

1. 先新增虛擬機的名稱  
<img decoding="async" src="https://i.imgur.com/pflnAFT.png" alt="" />  


2.名稱,系統,版本如下  
<img decoding="async" src="https://i.imgur.com/NPMNX72.png" alt="" /> 

以下步驟:  
記憶體大小(下一步)->立即建立虛擬硬碟->VDI(VirtualBox磁碟映像)->動態分配->建議分32G  
<img decoding="async" src="https://i.imgur.com/DqeBhjS.png" alt="" />  
<img decoding="async" src="https://i.imgur.com/IOpb9lK.png" alt="" /> 

新增完後點選設定:  
<img decoding="async" src="https://i.imgur.com/CXwIJuN.png" alt="" /> 

系統->加速->不要勾Nested Paging  
<img decoding="async" src="https://i.imgur.com/O0v2Pig.png" alt="" /> 

存放裝置 -> 空的 -> 找出iso檔的位置(自行決定要安裝的版本) -> 確定  
注意:iso檔盡量不要放在中文路徑的資料夾下  
<img decoding="async" src="https://i.imgur.com/Soak3kh.png" alt="" /> 

點選啟動:  
<img decoding="async" src="https://i.imgur.com/HSQeKe6.png" alt="" /> 

一開始的設定跟密碼不講解。

開始安裝畫面:  
<img decoding="async" src="https://i.imgur.com/Am90YfI.png" alt="" /> 

安裝完重新開機  
<img decoding="async" src="https://i.imgur.com/BZA6GoL.png" alt="" /> 

記得要按Enter進入系統，不然會一直停再畫面  
輸入剛剛設定時的密碼,記得打開右方的NumLock，不然可能按到&#8221;訪客作業階段&#8221;  
我設很簡單  
<img decoding="async" src="https://i.imgur.com/Vg4fEcS.png" alt="" /> 

登入成功!!!  
<img decoding="async" src="https://i.imgur.com/O3lFH3a.png" alt="" /> 

## <span class="ez-toc-section" id="%E8%A7%A3%E6%9E%90%E5%BA%A6%E8%A8%AD%E5%AE%9A"></span>解析度設定<span class="ez-toc-section-end"></span> 

畫面超級小,先把他調大一點…  
右上角->系統設定->顯示器->解析度(自行調整)  
我是用1680*1050(16:10)  
<img decoding="async" src="https://i.imgur.com/gQ6zMul.png" alt="" /> 

## <span class="ez-toc-section" id="%E8%A8%AD%E5%AE%9A%E5%8F%AF%E4%BB%A5%E9%9B%99%E5%90%91%E5%89%AA%E8%B2%BC"></span>設定可以雙向剪貼<span class="ez-toc-section-end"></span> 

沒用的話會無法貼上從windows複製的文字

裝置->插入Guest Additions CD 映像  
<img decoding="async" src="https://i.imgur.com/dZGRaKI.png" alt="" /> 

點選執行  
<img decoding="async" src="https://i.imgur.com/6LfMWVw.png" alt="" /> 

打上密碼:  
<img decoding="async" src="https://i.imgur.com/W5l12rr.png" alt="" />  
<img decoding="async" src="https://i.imgur.com/J1CMASF.png" alt="" />  


輸入:yes  
<img decoding="async" src="https://i.imgur.com/NAyT6hv.png" alt="" /> 

選雙向  
<img decoding="async" src="https://i.imgur.com/5sJV1uZ.png" alt="" />  
選雙向  
<img decoding="async" src="https://i.imgur.com/N84wRLB.png" alt="" /> 

完成

## <span class="ez-toc-section" id="%E5%85%B1%E4%BA%AB%E8%B3%87%E6%96%99%E5%A4%BE"></span>共享資料夾<span class="ez-toc-section-end"></span> 

終端機輸入這串:

<pre class="wp-block-code"><code lang="bash" class="language-bash">sudo usermod --append --groups vboxsf $USER</code></pre>

裝置-> 共用資料夾 -> 共用資料夾設定  
<img decoding="async" src="https://i.imgur.com/Iqf4SMG.png" alt="" /> 

注意:這裡選擇的是在外面windows的資料夾路徑  
<img decoding="async" src="https://i.imgur.com/lgV3Qtx.png" alt="" /> 

共用的資料夾是創建在windows的，  
不是ubuntu(如果想要從ubuntu分享也可以用其他方式)。  
<img decoding="async" src="https://i.imgur.com/e9KNlgz.png" alt="" /> 

下圖就是成功掛載的樣子，檢查資料夾的路徑，沒問題就按確認。  
<img decoding="async" src="https://i.imgur.com/u5Fi6H9.png" alt="" /> 

打開ubuntu的檔案資料夾，會出現剛才建立的資料夾:  
前綴是sf_加共用資料夾名稱，打開後測試看看能不能在ubuntu添加檔案。  
<img decoding="async" src="https://i.imgur.com/b8mvMBY.png" alt="" /> 



## <span class="ez-toc-section" id="%E7%95%AB%E9%9D%A2%E5%A4%A7%E5%B0%8F"></span>畫面大小<span class="ez-toc-section-end"></span> 

自動調整客體顯示大小  
<img decoding="async" src="https://i.imgur.com/0JyDeEU.png" alt="" /> 

##### 補充:無法使用客體大小 

某次安裝的ubuntu20.04無法使用客體大小。在網路上查了三個小時終於找到解決方式。

一直重新安裝VBoxGuestAdditions.iso檔都沒用，最後再下列網址找到解決方式。

[解決網址][1]  
終端機輸入下列指令，之後重新開機。

<pre class="wp-block-code"><code lang="bash" class="language-bash">sudo apt-get install virtualbox-guest-dkms</code></pre>

 [1]: https://askubuntu.com/questions/452979/resolution-doesnt-change-when-resizing-virtualbox-window