---
title: '[Windows] 美化Terminal- powershell'
author: Bocky
type: post
date: 2021-08-18T12:13:27+00:00
url: /2021/08/18/windows-美化terminal-powershell/
categories:
  - Terminal
tags:
  - terminal
  - Windows

---
<ol class="wp-block-list">
  <li>
    打開PowerShell<br />如果都沒有改過的話，windows預設的cmd是黑底白字，而PowerShell是藍底白字。<br /><img decoding="async" src="https://i.imgur.com/zS7p3tE.png" alt="" />
  </li>
  <li>
    oh-my-posh 安裝<br />打開 PowerShell，輸入下方兩行指令
  </li>
</ol>

<pre class="wp-block-code"><code lang="" class="">Install-Module posh-git -Scope CurrentUser
Install-Module oh-my-posh -Scope CurrentUser</code></pre>

都輸入:Y  
<img decoding="async" src="https://i.imgur.com/dINg6hQ.png" alt="" /> 

<ol class="wp-block-list" start="3">
  <li>
    在 PowerShell 上輸入 $PROFILE後輸入下列<br />用途:有檔案的話就開啟，沒有自動新增。
  </li>
</ol>

<pre class="wp-block-code"><code class="">if (!(Test-Path -Path $PROFILE )) { New-Item -Type File -Path $PROFILE -Force }</code></pre>

<ol class="wp-block-list" start="4">
  <li>
    使用VSCode開啟檔案:
  </li>
</ol>

<pre class="wp-block-code"><code class="">code $PROFILE</code></pre>

添加下方程式(除了前3個，其他可選用)後儲存，關閉PowerShell

<pre class="wp-block-code"><code class="">Import-Module posh-git
Import-Module oh-my-posh
Set-PoshPrompt -Theme Paradox</code></pre>

如果沒有安裝VSCode也沒關係，可以用其他文字編輯  
檔案路徑在，找到後再把剛才那三行複製貼上進去該檔案。

<pre class="wp-block-code"><code class="">C:\Users\你的電腦名稱\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1，器去打開它並新增。</code></pre>

<ol class="wp-block-list" start="5">
  <li>
    使用系統管理員開啟PowerShell<br />執行命令:
  </li>
</ol>

<pre class="wp-block-code"><code class="">Set-ExecutionPolicy RemoteSigned</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/sLa8q2l.png" alt="" /> </figure> 

<ol class="wp-block-list" start="6">
  <li>
    開啟Microsoft store<br />在放大鏡搜尋<code>Windows Terminal Preview</code><br /><img decoding="async" src="https://i.imgur.com/kxrtSlr.png" alt="" />
  </li>
</ol>

注意:在這裡要使用微軟的帳號登入才能下載，這邊沒有附上登入過程，請自行登入後再下載。  
<img decoding="async" src="https://i.imgur.com/HdYBhyB.png" alt="" /> 

成功後按啟動。  
<img decoding="async" src="https://i.imgur.com/32LeuZc.png" alt="" /> 

<ol class="wp-block-list" start="7">
  <li>
    啟動
  </li>
</ol>

打開可能會像下圖這一樣，有?的符號，下方會解決。  
<img decoding="async" src="https://i.imgur.com/YWiZNFE.png" alt="" /> 

目標是解決成下圖:  
<img decoding="async" src="https://i.imgur.com/lCOlq7j.png" alt="" /> 

如果過程有出現紅字:

<pre class="wp-block-code"><code class="">警告: git command could not be found. Please create an alias or add it to your PATH.</code></pre>

是找不到路徑，解決方式:安裝Git(請自行上網搜尋)

<ol class="wp-block-list" start="7">
  <li>
    下載字型包
  </li>
</ol>

到 powerline fonts 的 [github page][1] 下載字形包，用git下載或直接下載Zip檔後直接壓縮，都可以。

打開在資料夾的fonts-master\SourceCodePro，會看到很多.otf檔

找到Source Code Pro for Powerline.otf檔後，右鍵安裝。  
<img decoding="async" src="https://i.imgur.com/IJjenqL.png" alt="" /> 

再開啟控制台->外觀及個人化->字型<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/rxPd1hn.png" alt="" /> </figure> <figure class="wp-block-image"><img decoding="async" src="https://i.imgur.com/imHhkRd.png" alt="" /></figure> 

打開後會看到很多字型  
<img decoding="async" src="https://i.imgur.com/IBC0gGY.png" alt="" /> 

直接點放大鏡來搜尋，用Powerline來搜尋看看，  
確認是否安裝成功。  
<img decoding="async" src="https://i.imgur.com/qAVUwSL.png" alt="" /> 

<ol class="wp-block-list" start="8">
  <li>
    設定字型
  </li>
</ol>

打開設定  
<img decoding="async" src="https://i.imgur.com/QA7ta1V.png" alt="" /> 

點選左排的Windows PowerShell->外觀-> 顯示所有字型 -> 剛才安裝的字型:Source Code Pro for Powerline -> 儲存  
<img decoding="async" src="https://i.imgur.com/HAS43eC.png" alt="" /> 

<ol class="wp-block-list" start="9">
  <li>
    完成<br />回到Windows PowerShell按+後會出現一個新的<br /><img decoding="async" src="https://i.imgur.com/r4pK0kc.png" alt="" /><br /><img decoding="async" src="https://i.imgur.com/fR88Cd5.png" alt="" />
  </li>
</ol>

在8的步驟時，其實就可以做很多設定了，  
也可以直接去改setting.json檔  
<img decoding="async" src="https://i.imgur.com/qakySt0.png" alt="" /> 

如果想要看其他主題，可以輸入:

<pre class="wp-block-code"><code class="">Get-PoshThemes</code></pre>

 [1]: https://github.com/powerline/fonts