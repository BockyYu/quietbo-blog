---
title: '[C#]例外處理Exception'
author: Bocky
type: post
date: 2021-10-31T16:22:08+00:00
url: /2021/11/01/例外處理exception/
categories:
  - 'C# (no more update)'
tags:
  - 'C#'

---
[Microsoft： Exception 類別][1]  
程式執行期間發生的錯誤，會丟出異常或丟出例外。

例外處理是所有開發工程師必學的，以下介紹比較常見的 Exception

<ul class="wp-block-list">
  <li>
    確認例外的什麼類型
  </li>
  <li>
    透過debug來檢查是第幾行造成異常
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
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2021/11/01/%e4%be%8b%e5%a4%96%e8%99%95%e7%90%86exception/#NullReferenceException" >NullReferenceException</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2021/11/01/%e4%be%8b%e5%a4%96%e8%99%95%e7%90%86exception/#DivideByZeroException" >DivideByZeroException</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2021/11/01/%e4%be%8b%e5%a4%96%e8%99%95%e7%90%86exception/#ArgumentOutOfRangeException" >ArgumentOutOfRangeException</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2021/11/01/%e4%be%8b%e5%a4%96%e8%99%95%e7%90%86exception/#ArgumentNullException" >ArgumentNullException</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-5" href="https://quietbo.com/2021/11/01/%e4%be%8b%e5%a4%96%e8%99%95%e7%90%86exception/#FormatException" >FormatException</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-6" href="https://quietbo.com/2021/11/01/%e4%be%8b%e5%a4%96%e8%99%95%e7%90%86exception/#try%E2%80%A6catch%E2%80%A6finally" >try…catch…finally</a>
    </li>
  </ul></nav>
</div>

## <span class="ez-toc-section" id="NullReferenceException"></span>NullReferenceException<span class="ez-toc-section-end"></span> {.wp-block-heading}

當嘗試對Null 物件取值時，所擲回的例外狀況。

尋找字串裡，B在第幾個位置出現，由於name是null, 所以程式時會丟出例外，範例如下：

<pre class="wp-block-code"><code lang="csharp" class="language-csharp line-numbers">string name = null;
int position = name.IndexOf('B');</code></pre>

錯誤如下：

<pre class="wp-block-code"><code class="">Unhandled Exception:
System.NullReferenceException: Object reference not set to an instance of an object</code></pre>

## <span class="ez-toc-section" id="DivideByZeroException"></span>DivideByZeroException<span class="ez-toc-section-end"></span> {.wp-block-heading}

嘗試將整數或 Decimal 值除以零時，所擲回的例外狀況。

分母不可以為零，程式在執行時, 會丟出例外，範例如下：

<pre class="wp-block-code"><code lang="csharp" class="language-csharp">int i = 100;
int ans = i/0;</code></pre>

錯誤如下：

<pre class="wp-block-code"><code class="">System.DivideByZeroException: Attempted to divide by zero.</code></pre>

## <span class="ez-toc-section" id="ArgumentOutOfRangeException"></span>ArgumentOutOfRangeException<span class="ez-toc-section-end"></span> {.wp-block-heading}

引數超出有效值的範圍。

<pre class="wp-block-code"><code lang="csharp" class="language-csharp line-numbers">string value = "0123456789";

// 字串長度10, 叫用 Substring時, 傳入 100, 會丟出 ArgumentOutOfRangeException 例外
string result = value.Substring(100);</code></pre>

錯誤訊息如下：

<pre class="wp-block-code"><code class="">System.ArgumentOutOfRangeException: startIndex cannot be larger than length of string.</code></pre>

## <span class="ez-toc-section" id="ArgumentNullException"></span>ArgumentNullException<span class="ez-toc-section-end"></span> {.wp-block-heading}

[ArgumentNullException][2]  
當 Null 參考 (在 Visual Basic 中為 Nothing) 傳遞給不接受其為有效引數的方法時，所擲回的例外狀況。

不允許參數是null時,就會丟出ArgumentNullException

## <span class="ez-toc-section" id="FormatException"></span>FormatException<span class="ez-toc-section-end"></span> {.wp-block-heading}

引數格式無效或複合格式字串格式不正確時所擲回的例外狀況。

此用法是想使用字串插值，但因為語法錯誤，導致異常。

<pre class="wp-block-code"><code lang="csharp" class="language-csharp line-numbers">string template = "user_name: {bocky}"; 
string result = string.Format(template, "bocky");</code></pre>

錯誤如下：

<pre class="wp-block-code"><code class="">System.FormatException: Input string was not in a correct format.</code></pre>

## <span class="ez-toc-section" id="try%E2%80%A6catch%E2%80%A6finally"></span>try…catch…finally<span class="ez-toc-section-end"></span> {.wp-block-heading}

不要太依賴，若是能在開發時就想到需要檢查/判斷的地方，就先做好。

<ul class="wp-block-list">
  <li>
    <a href="https://docs.microsoft.com/zh-tw/dotnet/csharp/language-reference/keywords/try-catch">Microsoft：try-catch</a>
  </li>
  <li>
    <a href="https://docs.microsoft.com/zh-tw/dotnet/csharp/language-reference/keywords/try-finally">Microsoft：try-finally</a>
  </li>
  <li>
    <a href="https://docs.microsoft.com/zh-tw/dotnet/csharp/language-reference/keywords/try-catch-finally">Microsoft：try-catch-finally</a>
  </li>
</ul>

<pre class="wp-block-code"><code lang="csharp" class="language-csharp line-numbers">try
{
//程式執行區或可能發生異常的地方
}
catch (Exception ex)
{
//例外的處理方法，如秀出警告
}
finally
{
//無論是否有發生例外事件，都會執行這區塊
}</code></pre>

 [1]: https://docs.microsoft.com/zh-tw/dotnet/api/system.exception?view=net-5.0
 [2]: https://docs.microsoft.com/zh-tw/dotnet/api/system.argumentnullexception?view=net-5.0