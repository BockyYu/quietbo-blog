---
title: windows分享VPN給手機
author: Bocky
type: post
date: 2021-05-27T16:54:17+00:00
url: /2021/05/28/windows分享vpn給手機/
categories:
  - 系統相關

---
原本用手機測試都是連公司的wifi，不需要開vpn，但最近疫情關係要WFH，一定要用公司IP才能測試。

以下操作只要抓到兩個關鍵點就可以完成了  
1.VPN是哪台?如何判斷?  
2.如何開啟行動熱點?如何判斷?

<div id="ez-toc-container" class="ez-toc-v2_0_82_2 ez-toc-wrap-center counter-hierarchy ez-toc-counter ez-toc-grey ez-toc-container-direction">
  <div class="ez-toc-title-container">
    <p class="ez-toc-title" style="cursor:inherit">
      Table of Contents
    </p>
    
    <span class="ez-toc-title-toggle"><a href="#" class="ez-toc-pull-right ez-toc-btn ez-toc-btn-xs ez-toc-btn-default ez-toc-toggle" aria-label="顯示/隱藏內容目錄"><span class="ez-toc-js-icon-con"><span class=""><span class="eztoc-hide" style="display:none;">Toggle</span><span class="ez-toc-icon-toggle-span"><svg style="fill: #999;color:#999" xmlns="http://www.w3.org/2000/svg" class="list-377408" width="20px" height="20px" viewBox="0 0 24 24" fill="none"><path d="M6 6H4v2h2V6zm14 0H8v2h12V6zM4 11h2v2H4v-2zm16 0H8v2h12v-2zM4 16h2v2H4v-2zm16 0H8v2h12v-2z" fill="currentColor"></path></svg><svg style="fill: #999;color:#999" class="arrow-unsorted-368013" xmlns="http://www.w3.org/2000/svg" width="10px" height="10px" viewBox="0 0 24 24" version="1.2" baseProfile="tiny"><path d="M18.2 9.3l-6.2-6.3-6.2 6.3c-.2.2-.3.4-.3.7s.1.5.3.7c.2.2.4.3.7.3h11c.3 0 .5-.1.7-.3.2-.2.3-.5.3-.7s-.1-.5-.3-.7zM5.8 14.7l6.2 6.3 6.2-6.3c.2-.2.3-.5.3-.7s-.1-.5-.3-.7c-.2-.2-.4-.3-.7-.3h-11c-.3 0-.5.1-.7.3-.2.2-.3.5-.3.7s.1.5.3.7z"/></svg></span></span></span></a></span>
  </div><nav>
  
  <ul class='ez-toc-list ez-toc-list-level-1 ' >
    <li class='ez-toc-page-1 ez-toc-heading-level-1'>
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2021/05/28/windows%e5%88%86%e4%ba%abvpn%e7%b5%a6%e6%89%8b%e6%a9%9f/#%E9%96%8B%E5%95%9F%E7%B6%B2%E8%B7%AF%E9%80%A3%E7%B7%9A%E7%95%AB%E9%9D%A2" >開啟網路連線畫面</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-1'>
      <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2021/05/28/windows%e5%88%86%e4%ba%abvpn%e7%b5%a6%e6%89%8b%e6%a9%9f/#VPN%E6%98%AF%E5%93%AA%E5%8F%B0%E6%80%8E%E9%BA%BC%E5%88%A4%E6%96%B7" >VPN是哪台?怎麼判斷?</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-1'>
      <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2021/05/28/windows%e5%88%86%e4%ba%abvpn%e7%b5%a6%e6%89%8b%e6%a9%9f/#%E5%A6%82%E4%BD%95%E9%96%8B%E5%95%9F%E8%A1%8C%E5%8B%95%E7%86%B1%E9%BB%9E%E5%A6%82%E4%BD%95%E5%88%A4%E6%96%B7" >如何開啟行動熱點?如何判斷?</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-1'>
      <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2021/05/28/windows%e5%88%86%e4%ba%abvpn%e7%b5%a6%e6%89%8b%e6%a9%9f/#%E8%A8%AD%E5%AE%9A%E5%88%86%E4%BA%ABVPN%E6%AD%A5%E9%A9%9F" >設定分享VPN步驟</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-1'>
      <a class="ez-toc-link ez-toc-heading-5" href="https://quietbo.com/2021/05/28/windows%e5%88%86%e4%ba%abvpn%e7%b5%a6%e6%89%8b%e6%a9%9f/#%E6%B8%AC%E8%A9%A6" >測試</a>
    </li>
  </ul></nav>
</div>

# <span class="ez-toc-section" id="%E9%96%8B%E5%95%9F%E7%B6%B2%E8%B7%AF%E9%80%A3%E7%B7%9A%E7%95%AB%E9%9D%A2"></span>開啟網路連線畫面<span class="ez-toc-section-end"></span> 

先到下圖的畫面(如果找到了就可以跳過找這畫面的過程)  
<img decoding="async" src="https://i.imgur.com/oYrfG7N.png" alt="" /> 

如果找不到，可以在下方操作找到:  
右下網路WiFi圖示右鍵 -> 開啟網路和網際網路設定 -> 狀態 -> 變更介面卡選項  
<img decoding="async" src="https://i.imgur.com/dlQtPLh.png" alt="" />  
<img decoding="async" src="https://i.imgur.com/j8d2ED8.png" alt="" /> 

# <span class="ez-toc-section" id="VPN%E6%98%AF%E5%93%AA%E5%8F%B0%E6%80%8E%E9%BA%BC%E5%88%A4%E6%96%B7"></span>VPN是哪台?怎麼判斷?<span class="ez-toc-section-end"></span> 

看到後找尋有TAP-Windows Adapter V9 字的就是VPN。  
但若有2台以上，沒辦法判斷哪台才是真正要分享的VPN時，打開VPN的程式，再回來看網路連線，有連線上的就是正確的。  
<img decoding="async" src="https://i.imgur.com/vCaVmQK.png" alt="" /> 

# <span class="ez-toc-section" id="%E5%A6%82%E4%BD%95%E9%96%8B%E5%95%9F%E8%A1%8C%E5%8B%95%E7%86%B1%E9%BB%9E%E5%A6%82%E4%BD%95%E5%88%A4%E6%96%B7"></span>如何開啟行動熱點?如何判斷?<span class="ez-toc-section-end"></span> 

回到下面設定位置，開啟行動熱點，藍色框就是手機連線要找的Wifi名稱和密碼。  
<img decoding="async" src="https://i.imgur.com/oJg9ufU.png" alt="" /> 

回到網路連線畫面，會看到多了一個熱點分享的區域連線，這台就是要分享出去的網路，等等要設定，所以要記得名字。  
<img decoding="async" src="https://i.imgur.com/edYmhzv.png" alt="" /> 

# <span class="ez-toc-section" id="%E8%A8%AD%E5%AE%9A%E5%88%86%E4%BA%ABVPN%E6%AD%A5%E9%A9%9F"></span>設定分享VPN步驟<span class="ez-toc-section-end"></span> 

把已知VPN右鍵 -> 內容  
<img decoding="async" src="https://i.imgur.com/Kbdbsnm.png" alt="" /> 

共用 -> 第一個框打勾 -> 選擇行動熱點的區域連線  
<img decoding="async" src="https://i.imgur.com/1RcIzrL.png" alt="" /> 

# <span class="ez-toc-section" id="%E6%B8%AC%E8%A9%A6"></span>測試<span class="ez-toc-section-end"></span> 

把筆電和手機開啟<a href="https://www.whatismyip.com.tw/" target="_blank" rel="noreferrer noopener">測試網路IP的連結</a>，若IP一樣，就是分享成功!

參考連結:<a href="https://makingreal.net/win10%E7%94%B5%E8%84%91%E7%83%AD%E7%82%B9%E5%85%B1%E4%BA%ABvpn%E8%BF%9E%E7%BB%93/" target="_blank" rel="noreferrer noopener">Win10电脑热点共享VPN连结</a>