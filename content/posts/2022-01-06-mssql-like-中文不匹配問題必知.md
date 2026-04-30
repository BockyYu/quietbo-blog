---
title: '[MSSQL] like %%中文不匹配問題(必知)'
author: Bocky
type: post
date: 2022-01-06T08:33:23+00:00
url: /2022/01/06/mssql-like-中文不匹配問題必知/
categories:
  - Database
tags:
  - mssql

---
 

新手常犯，常忘記的匹配問題。主要是轉碼，需要在like後面添加個N，  
N轉換字符串爲nchar,nvarchar。<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/2Ivedf4.png" alt="" /> </figure> 

<pre class="wp-block-code"><code class="">SELECT [Type] ,[Title] FROM [TableName] WHERE [Title] LIKE N'%標題%'</code></pre>