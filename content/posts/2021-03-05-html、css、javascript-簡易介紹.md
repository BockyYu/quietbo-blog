---
title: HTML、CSS、JavaScript 簡易介紹
author: Bocky
type: post
date: 2021-03-05T06:55:55+00:00
url: /2021/03/05/html、css、javascript-簡易介紹/
categories:
  - Front-end(no more update)
tags:
  - CSS
  - HTML
  - JS

---
寫網頁時常聽到的三大名稱:

<blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow">
  <p>
    簡單來說:<br />html是網頁的結構，CSS是網頁的樣式，JavaScript是網頁的行為。
  </p>
</blockquote>

<ul class="wp-block-list">
  <li>
    HTML 網頁的結構，看起來都方方正正。
  </li>
  <li>
    CSS 把外貌給顯示出來，讓網頁的外貌看起來美觀一些
  </li>
  <li>
    JavaScript 控制網頁裡面的內容以及使用者的操作行為
  </li>
</ul>

<div id="ez-toc-container" class="ez-toc-v2_0_82_2 ez-toc-wrap-center counter-hierarchy ez-toc-counter ez-toc-grey ez-toc-container-direction">
  <div class="ez-toc-title-container">
    <p class="ez-toc-title" style="cursor:inherit">
      Table of Contents
    </p>
    
    <span class="ez-toc-title-toggle"><a href="#" class="ez-toc-pull-right ez-toc-btn ez-toc-btn-xs ez-toc-btn-default ez-toc-toggle" aria-label="顯示/隱藏內容目錄"><span class="ez-toc-js-icon-con"><span class=""><span class="eztoc-hide" style="display:none;">Toggle</span><span class="ez-toc-icon-toggle-span"><svg style="fill: #999;color:#999" xmlns="http://www.w3.org/2000/svg" class="list-377408" width="20px" height="20px" viewBox="0 0 24 24" fill="none"><path d="M6 6H4v2h2V6zm14 0H8v2h12V6zM4 11h2v2H4v-2zm16 0H8v2h12v-2zM4 16h2v2H4v-2zm16 0H8v2h12v-2z" fill="currentColor"></path></svg><svg style="fill: #999;color:#999" class="arrow-unsorted-368013" xmlns="http://www.w3.org/2000/svg" width="10px" height="10px" viewBox="0 0 24 24" version="1.2" baseProfile="tiny"><path d="M18.2 9.3l-6.2-6.3-6.2 6.3c-.2.2-.3.4-.3.7s.1.5.3.7c.2.2.4.3.7.3h11c.3 0 .5-.1.7-.3.2-.2.3-.5.3-.7s-.1-.5-.3-.7zM5.8 14.7l6.2 6.3 6.2-6.3c.2-.2.3-.5.3-.7s-.1-.5-.3-.7c-.2-.2-.4-.3-.7-.3h-11c-.3 0-.5.1-.7.3-.2.2-.3.5-.3.7s.1.5.3.7z"/></svg></span></span></span></a></span>
  </div><nav>
  
  <ul class='ez-toc-list ez-toc-list-level-1 ' >
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2021/03/05/html%e3%80%81css%e3%80%81javascript-%e7%b0%a1%e6%98%93%e4%bb%8b%e7%b4%b9/#HTML_%E5%9F%BA%E6%9C%AC%E8%A7%80%E5%BF%B5" >HTML 基本觀念</a><ul class='ez-toc-list-level-3' >
        <li class='ez-toc-heading-level-3'>
          <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2021/03/05/html%e3%80%81css%e3%80%81javascript-%e7%b0%a1%e6%98%93%e4%bb%8b%e7%b4%b9/#%E5%B7%A2%E7%8B%80%E7%B5%90%E6%A7%8B" >巢狀結構</a>
        </li>
        <li class='ez-toc-page-1 ez-toc-heading-level-3'>
          <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2021/03/05/html%e3%80%81css%e3%80%81javascript-%e7%b0%a1%e6%98%93%e4%bb%8b%e7%b4%b9/#%E5%85%83%E7%B4%A0element" >元素(element)</a>
        </li>
        <li class='ez-toc-page-1 ez-toc-heading-level-3'>
          <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2021/03/05/html%e3%80%81css%e3%80%81javascript-%e7%b0%a1%e6%98%93%e4%bb%8b%e7%b4%b9/#%E5%B1%AC%E6%80%A7attribute" >屬性(attribute)</a>
        </li>
      </ul>
    </li>
    
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-5" href="https://quietbo.com/2021/03/05/html%e3%80%81css%e3%80%81javascript-%e7%b0%a1%e6%98%93%e4%bb%8b%e7%b4%b9/#CSS" >CSS</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-6" href="https://quietbo.com/2021/03/05/html%e3%80%81css%e3%80%81javascript-%e7%b0%a1%e6%98%93%e4%bb%8b%e7%b4%b9/#JavaScript_%E2%80%93_JS" >JavaScript &#8211; JS</a>
    </li>
  </ul></nav>
</div>

## <span class="ez-toc-section" id="HTML_%E5%9F%BA%E6%9C%AC%E8%A7%80%E5%BF%B5"></span>HTML 基本觀念<span class="ez-toc-section-end"></span> 

<ul class="wp-block-list">
  <li>
    巢狀結構
  </li>
  <li>
    元素(element)
  </li>
  <li>
    屬性(attribute)<br />使用文本編輯軟件即可做開發，以 .html 或 .htm 為結尾的文件，最後使用瀏覽器開啟檔案即可顯示。
  </li>
</ul>

### <span class="ez-toc-section" id="%E5%B7%A2%E7%8B%80%E7%B5%90%E6%A7%8B"></span>巢狀結構<span class="ez-toc-section-end"></span> 

簡單來說就是一層一層的概念  
範例:

<pre class="wp-block-code"><code lang="markup" class="language-markup">&lt;html&gt;
    &lt;head&gt;
        &lt;title&gt;Title&lt;/title&gt;
    &lt;/head&gt;
    &lt;body&gt;
        &lt;h1&gt;標題H1 &lt;/h1&gt;
    &lt;/body&gt;
&lt;/html&gt;</code></pre>

因為巢狀結構有分層級，上層稱為`父元素`，下層稱為`子元素`。  
而層級之間有一定上下、左右的規則，會透過`Document Object Model (DOM)`來進行遍歷的順序。

### <span class="ez-toc-section" id="%E5%85%83%E7%B4%A0element"></span>元素(element)<span class="ez-toc-section-end"></span> 

使用過程中，需要用 <> 括起來。  
[HTML元素網址][1]

### <span class="ez-toc-section" id="%E5%B1%AC%E6%80%A7attribute"></span>屬性(attribute)<span class="ez-toc-section-end"></span> 

可以藉由各種方式去設定元素或調整它們的行為。  
簡單來說，除了最開頭的元素以外，中間都是屬性。

[HTML屬性網址][2]

## <span class="ez-toc-section" id="CSS"></span>CSS<span class="ez-toc-section-end"></span> 

CSS就是管理網頁的外貌。

<pre class="wp-block-code"><code lang="css" class="language-css">.mainBody{
    min-width: 1024px;
    width: 100%;
    height: 100%;
}
.mainBody .logo{
    height: 45px;
    line-height: 45px;
    background-color: #214D8A;
}</code></pre>

## <span class="ez-toc-section" id="JavaScript_%E2%80%93_JS"></span>JavaScript &#8211; JS<span class="ez-toc-section-end"></span> 

JavaScript 就是管理網頁的內容以及使用者的操作行為，為了要控制網頁的內容。

<pre class="wp-block-code"><code lang="javascript" class="language-javascript">&lt;script&gt;
&lt;/script&gt;</code></pre>

就是實做JavaScript的地方。

 [1]: https://developer.mozilla.org/zh-TW/docs/Web/HTML/Element
 [2]: https://developer.mozilla.org/zh-TW/docs/Web/HTML/Attributes