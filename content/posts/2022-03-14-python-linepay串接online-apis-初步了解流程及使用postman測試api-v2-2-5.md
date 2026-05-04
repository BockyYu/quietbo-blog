---
title: '[Python] LinePay串接Online APIs – 初步了解流程及使用postman測試api v2 (2/5)'
author: Bocky
type: post
date: 2022-03-13T17:22:34+00:00
url: /2022/03/14/python-linepay串接online-apis-初步了解流程及使用postman測試api-v2-2-5/
categories:
  - Python
tags:
  - linepay

---
因有些人只想了解linepay的運作方式, 提供一些簡單可使用的方式。

以下測試環境及工具使用:

<ul class="wp-block-list">
  <li>
    Sandbox
  </li>
  <li>
    postman
  </li>
  <li>
    linePay文檔
  </li>
  <li>
    Online APIs 文檔:<a href="https://pay.line.me/tw/developers/apis/onlineApis?locale=zh_TW">網址</a>
  </li>
  <li>
    按下<a href="https://pay.line.me/documents/online_v2_en.html">此處</a> 查看以前的API文件(v2)
  </li>
</ul>

本次postman的簡易流程  
簡易流程圖[網址][1]  
<img decoding="async" src="https://i.imgur.com/N2ftauj.jpg" alt="" /> 

<div id="ez-toc-container" class="ez-toc-v2_0_82_2 ez-toc-wrap-center counter-hierarchy ez-toc-counter ez-toc-grey ez-toc-container-direction">
  <div class="ez-toc-title-container">
    <p class="ez-toc-title" style="cursor:inherit">
      Table of Contents
    </p>
    
    <span class="ez-toc-title-toggle"><a href="#" class="ez-toc-pull-right ez-toc-btn ez-toc-btn-xs ez-toc-btn-default ez-toc-toggle" aria-label="顯示/隱藏內容目錄"><span class="ez-toc-js-icon-con"><span class=""><span class="eztoc-hide" style="display:none;">Toggle</span><span class="ez-toc-icon-toggle-span"><svg style="fill: #999;color:#999" xmlns="http://www.w3.org/2000/svg" class="list-377408" width="20px" height="20px" viewBox="0 0 24 24" fill="none"><path d="M6 6H4v2h2V6zm14 0H8v2h12V6zM4 11h2v2H4v-2zm16 0H8v2h12v-2zM4 16h2v2H4v-2zm16 0H8v2h12v-2z" fill="currentColor"></path></svg><svg style="fill: #999;color:#999" class="arrow-unsorted-368013" xmlns="http://www.w3.org/2000/svg" width="10px" height="10px" viewBox="0 0 24 24" version="1.2" baseProfile="tiny"><path d="M18.2 9.3l-6.2-6.3-6.2 6.3c-.2.2-.3.4-.3.7s.1.5.3.7c.2.2.4.3.7.3h11c.3 0 .5-.1.7-.3.2-.2.3-.5.3-.7s-.1-.5-.3-.7zM5.8 14.7l6.2 6.3 6.2-6.3c.2-.2.3-.5.3-.7s-.1-.5-.3-.7c-.2-.2-.4-.3-.7-.3h-11c-.3 0-.5.1-.7.3-.2.2-.3.5-.3.7s.1.5.3.7z"/></svg></span></span></span></a></span>
  </div><nav>
  
  <ul class='ez-toc-list ez-toc-list-level-1 ' >
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2022/03/14/python-linepay%e4%b8%b2%e6%8e%a5online-apis-%e5%88%9d%e6%ad%a5%e4%ba%86%e8%a7%a3%e6%b5%81%e7%a8%8b%e5%8f%8a%e4%bd%bf%e7%94%a8postman%e6%b8%ac%e8%a9%a6api-v2-2-5/#%E5%9F%BA%E6%9C%AC%E8%A8%AD%E5%AE%9A" >基本設定</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2022/03/14/python-linepay%e4%b8%b2%e6%8e%a5online-apis-%e5%88%9d%e6%ad%a5%e4%ba%86%e8%a7%a3%e6%b5%81%e7%a8%8b%e5%8f%8a%e4%bd%bf%e7%94%a8postman%e6%b8%ac%e8%a9%a6api-v2-2-5/#request_%E8%AB%8B%E6%B1%82%E8%A8%82%E5%96%AE" >request 請求訂單</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2022/03/14/python-linepay%e4%b8%b2%e6%8e%a5online-apis-%e5%88%9d%e6%ad%a5%e4%ba%86%e8%a7%a3%e6%b5%81%e7%a8%8b%e5%8f%8a%e4%bd%bf%e7%94%a8postman%e6%b8%ac%e8%a9%a6api-v2-2-5/#confirm_%E7%A2%BA%E8%AA%8D" >confirm 確認</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2022/03/14/python-linepay%e4%b8%b2%e6%8e%a5online-apis-%e5%88%9d%e6%ad%a5%e4%ba%86%e8%a7%a3%e6%b5%81%e7%a8%8b%e5%8f%8a%e4%bd%bf%e7%94%a8postman%e6%b8%ac%e8%a9%a6api-v2-2-5/#Check_Payment_Status_%E6%9F%A5%E7%9C%8B%E8%A8%82%E5%96%AE%E7%8B%80%E6%85%8B" >Check Payment Status 查看訂單狀態</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-5" href="https://quietbo.com/2022/03/14/python-linepay%e4%b8%b2%e6%8e%a5online-apis-%e5%88%9d%e6%ad%a5%e4%ba%86%e8%a7%a3%e6%b5%81%e7%a8%8b%e5%8f%8a%e4%bd%bf%e7%94%a8postman%e6%b8%ac%e8%a9%a6api-v2-2-5/#refurnd_%E9%80%80%E6%AC%BE" >refurnd 退款</a>
    </li>
  </ul></nav>
</div>

## <span class="ez-toc-section" id="%E5%9F%BA%E6%9C%AC%E8%A8%AD%E5%AE%9A"></span>基本設定<span class="ez-toc-section-end"></span> 

請先下載[postman][2]

**domain**(v2測試用)

<pre class="wp-block-code"><code class="">https://sandbox-api-pay.line.me/v2/payments</code></pre>

在現有的**Headers**添加

<pre class="wp-block-code"><code lang="json" class="language-json line-numbers">Content-Type:application/json
X-LINE-ChannelId:商戶的Channel ID
X-LINE-ChannelSecret:商戶的Channel Secret</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/xwo8UJj.png" alt="" /> </figure> 

## <span class="ez-toc-section" id="request_%E8%AB%8B%E6%B1%82%E8%A8%82%E5%96%AE"></span>request 請求訂單<span class="ez-toc-section-end"></span> 

API:

<pre class="wp-block-code"><code lang="bash" class="language-bash">POST {domain}/request</code></pre>

Request Body:

<pre class="wp-block-code"><code lang="json" class="language-json line-numbers">{
    "amount": 1,
    "currency": "TWD", 
    "productName": "MyProd",
    "productImageUrl": "https://cimg.cnyes.cool/prod/news/4556115/l/79b7b76238dcaa28d626ec007bff576f.jpg",
    "confirmUrl": "http://127.0.0.1:3000",
    "orderId": "Order202203110011"
}</code></pre>

Payment Reserve Response:

<pre class="wp-block-code"><code lang="json" class="language-json line-numbers">{
    "returnCode": "0000",
    "returnMessage": "Success.",
    "info": {
        "paymentUrl": {
            "web": "https://sandbox-web-pay.line.me/web/payment/wait?transactionReserveId=WVZub2tRakxRbzk0NWVsa1VMZ1pyTzhOSk00QXJqNXgvbTZIeXZ2NklpL2ZiMHlBUGN4SnJrTG4xVWh6bFA1cg",
            "app": "line://pay/payment/WVZub2tRakxRbzk0NWVsa1VMZ1pyTzhOSk00QXJqNXgvbTZIeXZ2NklpL2ZiMHlBUGN4SnJrTG4xVWh6bFA1cg"
        },
        "transactionId": 2022031100707222710,
        "paymentAccessToken": "785453599850"
    }
}</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/TRf6Xju.png" alt="" /> </figure> 

取得info.paymentUrl.web後, 使用瀏覽器打開如下:  
<img decoding="async" src="https://i.imgur.com/KqzzWBQ.png" alt="" /> 

點擊付款:  
<img decoding="async" src="https://i.imgur.com/96WKw9t.png" alt="" /> 

付款成功如下:  
<img decoding="async" src="https://i.imgur.com/iqFRyLj.png" alt="" /> 

補充:  
為什麼結帳後會原本的網頁會出現下圖?  
<img decoding="async" src="https://i.imgur.com/fSpv3o3.png" alt="" /> 

文檔內的說明如下

<pre class="wp-block-code"><code lang="bash" class="language-bash">Merchant's URL that the buyer is redirected to after selecting a payment method and entering the payment password in LINE Pay.
On the redirected URL, Merchant can call Confirm Payment API and complete the payment
LINE Pay passes an additional parameter, "transactionId"

Reference Detailed Explanation and Exceptional Case of ConfirmUrl</code></pre>

簡單來說就是:想讓結帳完的顧客看到什麼畫面。

## <span class="ez-toc-section" id="confirm_%E7%A2%BA%E8%AA%8D"></span>confirm 確認<span class="ez-toc-section-end"></span> 

API:

<pre class="wp-block-code"><code lang="bash" class="language-bash">POST {domain}/{transactionId}/confirm</code></pre>

範例:

<pre class="wp-block-code"><code lang="bash" class="language-bash">https://sandbox-api-pay.line.me/v2/payments/2022031400707322810/confirm</code></pre>

**Headers**添加

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">X-LINE-MerchantDeviceType: POS
X-LINE-MerchantDeviceProfileId: DUMMY</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/zX0wqPs.png" alt="" /> </figure> 

Request Body:

<pre class="wp-block-code"><code lang="json" class="language-json line-numbers">{
    "amount": 1,
    "currency": "TWD"
}</code></pre>

Response成功的Json如下:  
(補充:此次訂單是重新發起的新的訂單,所以transactionId與orderId會與上面請求訂單時的資料不一樣, 主要目的是呈現成功的結果)

<pre class="wp-block-code"><code lang="json" class="language-json line-numbers">{
    "returnCode": "0000",
    "returnMessage": "Success.",
    "info": {
        "transactionId": 2022031400707322810,
        "orderId": "dev202203140002",
        "payInfo": [
            {
                "method": "CREDIT_CARD",
                "amount": 1,
                "maskedCreditCardNumber": "************1111"
            }
        ]
    }
}</code></pre>

若失敗或是orderId有重複, 則會告知錯誤。

## <span class="ez-toc-section" id="Check_Payment_Status_%E6%9F%A5%E7%9C%8B%E8%A8%82%E5%96%AE%E7%8B%80%E6%85%8B"></span>Check Payment Status 查看訂單狀態<span class="ez-toc-section-end"></span> 

API

<pre class="wp-block-code"><code lang="bash" class="language-bash">GET {domain}?transactionId={transactionId}</code></pre>

範例:

<pre class="wp-block-code"><code lang="bash" class="language-bash">https://sandbox-api-pay.line.me/v2/payments?transactionId=2022031400707322810</code></pre>

Response成功的Json如下:

<pre class="wp-block-code"><code lang="json" class="language-json line-numbers">{
    "returnCode": "0000",
    "returnMessage": "Success.",
    "info": [
        {
            "transactionId": 2022031400707322810,
            "transactionDate": "2022-03-13T16:11:08Z",
            "transactionType": "PAYMENT",
            "productName": "MyProd",
            "currency": "TWD",
            "payInfo": [
                {
                    "method": "CREDIT_CARD",
                    "amount": 1
                }
            ],
            "orderId": "dev202203140002"
        }
    ]
}</code></pre>

注意:  
正常來說是要先檢查是否付款後才執行confirm這支API，但因為v2是需要先進行confirm這支API才有辦法使用，否則會出現:

<pre class="wp-block-code"><code lang="json" class="language-json line-numbers">{
    "returnCode": "1150",
    "returnMessage": "Transaction record not found."
}</code></pre>

若是使用v3則可正常先進行Check Payment Status 後再進行確認。

## <span class="ez-toc-section" id="refurnd_%E9%80%80%E6%AC%BE"></span>refurnd 退款<span class="ez-toc-section-end"></span> 

取消已付款的交易。

API:

<pre class="wp-block-code"><code lang="bash" class="language-bash">POST {dimain}/{transactionId}/refund</code></pre>

**Headers**添加

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">X-LINE-MerchantDeviceType: POS
X-LINE-MerchantDeviceProfileId: DUMMY</code></pre>

refundAmount: 退款金額

<pre class="wp-block-code"><code lang="json" class="language-json line-numbers">{
    "refundAmount": 1
}</code></pre>

Response:

<pre class="wp-block-code"><code lang="json" class="language-json line-numbers">{
    "returnCode": "0000",
    "returnMessage": "Success.",
    "info": {
        "refundTransactionId": 2022031400707327211,
        "refundTransactionDate": "2022-03-13T17:05:50Z"
    }
}</code></pre>

 [1]: https://i.imgur.com/N2ftauj.jpg
 [2]: https://www.postman.com/