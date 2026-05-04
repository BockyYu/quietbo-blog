---
title: '[Postman] Mock Servers(含圖和Json)'
author: Bocky
type: post
date: 2023-01-19T09:32:19+00:00
url: /2023/01/19/postman-mock-servers含圖和json/
categories:
  - 工具類
tags:
  - mock servers
  - Postman

---
為何需要使用到Mock?  
可參考這篇[\[面試\]\[後端\]在正式 API 完成前，如何讓要串接的工程師不要空等？][1]

不只是前端可能會遇到要等後端API完成，有時候後端要與其他Server對接API拿資料時，也會使用到。  
當不只是一個部門再開發時，可能需要與其他部門合作，等待對接API資料時，也能有效提高開發速度，避免在那等來等去的。

<div id="ez-toc-container" class="ez-toc-v2_0_82_2 ez-toc-wrap-center counter-hierarchy ez-toc-counter ez-toc-grey ez-toc-container-direction">
  <div class="ez-toc-title-container">
    <p class="ez-toc-title" style="cursor:inherit">
      Table of Contents
    </p>
    
    <span class="ez-toc-title-toggle"><a href="#" class="ez-toc-pull-right ez-toc-btn ez-toc-btn-xs ez-toc-btn-default ez-toc-toggle" aria-label="顯示/隱藏內容目錄"><span class="ez-toc-js-icon-con"><span class=""><span class="eztoc-hide" style="display:none;">Toggle</span><span class="ez-toc-icon-toggle-span"><svg style="fill: #999;color:#999" xmlns="http://www.w3.org/2000/svg" class="list-377408" width="20px" height="20px" viewBox="0 0 24 24" fill="none"><path d="M6 6H4v2h2V6zm14 0H8v2h12V6zM4 11h2v2H4v-2zm16 0H8v2h12v-2zM4 16h2v2H4v-2zm16 0H8v2h12v-2z" fill="currentColor"></path></svg><svg style="fill: #999;color:#999" class="arrow-unsorted-368013" xmlns="http://www.w3.org/2000/svg" width="10px" height="10px" viewBox="0 0 24 24" version="1.2" baseProfile="tiny"><path d="M18.2 9.3l-6.2-6.3-6.2 6.3c-.2.2-.3.4-.3.7s.1.5.3.7c.2.2.4.3.7.3h11c.3 0 .5-.1.7-.3.2-.2.3-.5.3-.7s-.1-.5-.3-.7zM5.8 14.7l6.2 6.3 6.2-6.3c.2-.2.3-.5.3-.7s-.1-.5-.3-.7c-.2-.2-.4-.3-.7-.3h-11c-.3 0-.5.1-.7.3-.2.2-.3.5-.3.7s.1.5.3.7z"/></svg></span></span></span></a></span>
  </div><nav>
  
  <ul class='ez-toc-list ez-toc-list-level-1 ' >
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2023/01/19/postman-mock-servers%e5%90%ab%e5%9c%96%e5%92%8cjson/#%E5%BB%BA%E7%AB%8B_Mock_Server" >建立 Mock Server</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2023/01/19/postman-mock-servers%e5%90%ab%e5%9c%96%e5%92%8cjson/#%E8%A8%AD%E8%A8%88_Mock_Server_Response" >設計 Mock Server Response</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2023/01/19/postman-mock-servers%e5%90%ab%e5%9c%96%e5%92%8cjson/#response_%E7%B5%A6%E9%9A%A8%E6%A9%9F%E8%B3%87%E6%96%99" >response 給隨機資料</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2023/01/19/postman-mock-servers%e5%90%ab%e5%9c%96%e5%92%8cjson/#%E4%BE%9D%E7%8B%80%E6%B3%81%E8%BF%94%E5%9B%9E%E4%B8%8D%E5%90%8C%E7%9A%84Response" >依狀況返回不同的Response</a><ul class='ez-toc-list-level-3' >
        <li class='ez-toc-heading-level-3'>
          <a class="ez-toc-link ez-toc-heading-5" href="https://quietbo.com/2023/01/19/postman-mock-servers%e5%90%ab%e5%9c%96%e5%92%8cjson/#%E6%88%90%E5%8A%9F%E5%A4%B1%E6%95%97%E7%9A%84%E8%BF%94%E5%9B%9E%E6%96%B9%E5%BC%8F" >成功/失敗的返回方式</a>
        </li>
      </ul>
    </li>
  </ul></nav>
</div>

## <span class="ez-toc-section" id="%E5%BB%BA%E7%AB%8B_Mock_Server"></span>建立 Mock Server<span class="ez-toc-section-end"></span> <figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/tlZXWGc.png" alt="" /> </figure> <figure class="wp-block-image"><img decoding="async" src="https://i.imgur.com/DtEhwsl.png" alt="" /></figure> 

建議勾選儲存 mock server URL 到環境變數的選項。  
<img decoding="async" src="https://i.imgur.com/HYsA4d3.png" alt="" /> 

創建成功左方會新增一個Mock及mock server URL  
<img decoding="async" src="https://i.imgur.com/Lw4845M.png" alt="" /> 

點擊左方的Environments會有剛才建立的Mock Server Name，會自動將mock server URL帶入到url內，  
後續只要打{{url}}就會取得資訊。  
<img decoding="async" src="https://i.imgur.com/K34Mzma.png" alt="" /> 

## <span class="ez-toc-section" id="%E8%A8%AD%E8%A8%88_Mock_Server_Response"></span>設計 Mock Server Response<span class="ez-toc-section-end"></span> 

<ol class="wp-block-list">
  <li>
    到Collections的分頁
  </li>
  <li>
    找到剛剛初始化的 Request，{{url}}會自動帶入
  </li>
  <li>
    環境變數右上角請選擇剛剛建立的「User」
  </li>
  <li>
    按下Send後
  </li>
  <li>
    下面的Response一片空白是正常的，因為還沒設定 Mock Server Response
  </li>
</ol><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/w1RrUNa.png" alt="" /> </figure> 

左側 Request 下面有一個「Default」，它就是用來自訂Response example，  
最下方改為Json輸入完後儲存:

<pre class="wp-block-code"><code lang="json" class="language-json line-numbers">{
    "id":1,
    "user": "bocky"
}</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/56BeBvI.png" alt="" /> </figure> 

回到Request，按下Send後，Response會跟剛剛填寫Json相同:  
<img decoding="async" src="https://i.imgur.com/7ba9mw3.png" alt="" /> 

## <span class="ez-toc-section" id="response_%E7%B5%A6%E9%9A%A8%E6%A9%9F%E8%B3%87%E6%96%99"></span>response 給隨機資料<span class="ez-toc-section-end"></span> 

Postman 本身就有提供給隨機資料的參數，主要在 example response 那邊把固定值改填參數就行，在 [文件][2] 中給的範例是這樣：

<pre class="wp-block-code"><code lang="json" class="language-json line-numbers">{
  "name": "{{$randomFullName}}",
  "userName": "{{$randomUserName}}",
  "location": "{{$randomCity}}",
  "company": "{{$randomCompanyName}}",
  "jobTitle": "{{$randomJobTitle}}",
  "updatedAt": "{{$timestamp}}"
}</code></pre>

收到的 response 就會像這樣：  
<img decoding="async" src="https://i.imgur.com/3Y6wP1r.png" alt="" /> 

<pre class="wp-block-code"><code lang="json" class="language-json line-numbers">{
    "name": "Mrs. Dana Berge",
    "userName": "Natalie.Moen85",
    "location": "South Orlando",
    "company": "Bergstrom, Schultz and O'Conner",
    "jobTitle": "Forward Data Manager",
    "updatedAt": "1674070363"
}</code></pre>

Postman 有的隨機參數官方都整理在這：[Dynamic variables][3]

## <span class="ez-toc-section" id="%E4%BE%9D%E7%8B%80%E6%B3%81%E8%BF%94%E5%9B%9E%E4%B8%8D%E5%90%8C%E7%9A%84Response"></span>依狀況返回不同的Response<span class="ez-toc-section-end"></span> 

通常在不同狀況會有不同的Response，例如成功或失敗。

### <span class="ez-toc-section" id="%E6%88%90%E5%8A%9F%E5%A4%B1%E6%95%97%E7%9A%84%E8%BF%94%E5%9B%9E%E6%96%B9%E5%BC%8F"></span>成功/失敗的返回方式<span class="ez-toc-section-end"></span> 

再新增一個Explore為失敗的UserNume(success)。  
當data為success時，返回:

<pre class="wp-block-code"><code lang="json" class="language-json line-numbers">{
    "status": "success",
    "msg": "成功",
    "data": {
        "name": "{{$randomFullName}}",
        "userName": "{{$randomUserName}}",
        "location": "{{$randomCity}}",
        "company": "{{$randomCompanyName}}",
        "jobTitle": "{{$randomJobTitle}}",
        "updatedAt": "{{$timestamp}}"
    }
}</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/173Jsgi.png" alt="" /> </figure> 

再新增一個Explore為失敗的UserNume(Error)。  
當data為error時的Response為

<pre class="wp-block-code"><code lang="json" class="language-json line-numbers">{
    "status": "error",
    "msg": "失敗",
    "data": {}
}</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/gXVklT2.png" alt="" /> </figure> 

測試成功Response:  
<img decoding="async" src="https://i.imgur.com/DqSzD5e.png" alt="" /> 

測試失敗的Response:  
<img decoding="async" src="https://i.imgur.com/VsbOQJm.png" alt="" />

 [1]: https://ithelp.ithome.com.tw/articles/10267680
 [2]: https://learning.postman.com/docs/designing-and-developing-your-api/mocking-data/mocking-with-examples/
 [3]: https://learning.postman.com/docs/writing-scripts/script-references/variables-list/