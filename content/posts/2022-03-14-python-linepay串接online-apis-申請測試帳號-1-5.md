---
title: '[Python] LinePay串接Online APIs – 申請測試帳號 (1/5)'
author: Bocky
type: post
date: 2022-03-13T17:17:51+00:00
url: /2022/03/14/python-linepay串接online-apis-申請測試帳號-1-5/
categories:
  - Python
tags:
  - linepay

---
以下測試環境使用:

<ul class="wp-block-list">
  <li>
    Sandbox
  </li>
</ul>

## 一、創建Sandbox帳號 {.wp-block-heading}

[測試流程文件網址][1]

<ul class="wp-block-list">
  <li>
    LinePay建立Sandbox:<a href="https://pay.line.me/tw/developers/techsupport/sandbox/testflow?locale=zh_TW">Sandbox網址</a>
  </li>
  <li>
    正式LinePay商戶請使用:<a href="https://pay.line.me/portal/tw/main?isFooterConventionChanged=true">網址</a>
  </li>
</ul>

填入下方訊息, 及使用中的信箱, 此處我是使用與line相同的信箱，若是以有相同信箱會跳出:此email已註冊過Sandbox ID。請輸入其他email以註冊Sandbox。  
<img decoding="async" src="https://i.imgur.com/wxZlyNd.png" alt="" /> 

創建成功如下圖(有興趣可自行點擊後查看)  
<img decoding="async" src="https://i.imgur.com/TyR7AIv.png" alt="" /> 

## 二、收信並登入商家 {.wp-block-heading}

到信箱收信如下:  
<img decoding="async" src="https://i.imgur.com/agbkGVt.png" alt="" /> 

使用剛才收到的來登入Merchant Center:[網址][2]

使用收到的測試帳號及密碼登入  
<img decoding="async" src="https://i.imgur.com/ABRSthV.png" alt="" /> 

## 三、取得Channel ID及Channel Secret Key {.wp-block-heading}<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/xVp3hpJ.png" alt="" /> </figure> 

紅框內的要保留好, 不要外流。  
<img decoding="async" src="https://i.imgur.com/hcN9p8I.png" alt="" /> 

補充:

<pre class="wp-block-code"><code class="">Sandbox: 指測試帳號的url及後台等等環境
v2/v3指的是在串接api時的linepay版本</code></pre>

 [1]: https://pay.line.me/tw/developers/techsupport/sandbox/testflow?locale=zh_TW
 [2]: https://pay.line.me/portal/tw/auth/login#