---
title: '[C#] 建置一個Hello world'
author: Bocky
type: post
date: 2021-09-21T06:57:13+00:00
url: /2021/09/21/c-建置一個hello-world-新手教學1/
categories:
  - 'C# (no more update)'
tags:
  - 'C#'

---
環境:Windows  
IDE: VS2019

## 建置一個C#專案來顯示Hello world 

<ol class="wp-block-list">
  <li>
    開啟VS2019 (Visual Studio 2019)
  </li>
</ol><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/bQCe6MN.png" alt="" /> </figure> 

<ol class="wp-block-list" start="2">
  <li>
    開啟新的專案
  </li>
</ol><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/nYWaSE2.png" alt="" /> </figure> 

<ol class="wp-block-list" start="3">
  <li>
    建立專案
  </li>
</ol><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/2gAkOLz.png" alt="" /> </figure> <figure class="wp-block-image"><img decoding="async" src="https://i.imgur.com/T2QPiHi.png" alt="" /></figure> 

<ol class="wp-block-list" start="4">
  <li>
    添加一行要顯示的文字
  </li>
</ol>

在Main裡面(第12~14行)中間填入:

<pre class="wp-block-code"><code lang="csharp" class="language-csharp line-numbers">Console.WriteLine("Hello world");</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/EoPdfsz.png" alt="" /> </figure> 

一定要按下儲存(Ctrl+S)  
<img decoding="async" src="https://i.imgur.com/agfE2kz.png" alt="" /> 

<ol class="wp-block-list" start="4">
  <li>
    建置/重建方案
  </li>
</ol>

<img decoding="async" src="https://i.imgur.com/q7MzcI1.png" alt="" />  
注意:不要有失敗  
<img decoding="async" src="https://i.imgur.com/ConnLgf.png" alt="" /> 

<ol class="wp-block-list" start="5">
  <li>
    執行
  </li>
</ol>

偵錯-> 啟動但不偵錯  
<img decoding="async" src="https://i.imgur.com/uxTlUyR.png" alt="" />  
會跳出一個終端機，顯示Hello world  
<img decoding="async" src="https://i.imgur.com/3zF60gf.png" alt="" />