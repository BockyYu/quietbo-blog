---
title: '[Python] break、continue、pass、return及exit的用法與區別'
author: Bocky
type: post
date: 2021-11-04T16:53:04+00:00
url: /2021/11/05/python-break、continue、pass、return及exit的用法與區別/
categories:
  - Python
tags:
  - python
  - 基本功

---
<ul class="wp-block-list">
  <li>
    break 結束循環語句
  </li>
  <li>
    continue 跳出本次循環，繼續下一個循環
  </li>
  <li>
    pass 不做任何事情，站位而已
  </li>
  <li>
    return 退出整個函數(def)
  </li>
  <li>
    exit 結束整個程序(進程)
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
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2021/11/05/python-break%e3%80%81continue%e3%80%81pass%e3%80%81return%e5%8f%8aexit%e7%9a%84%e7%94%a8%e6%b3%95%e8%88%87%e5%8d%80%e5%88%a5/#break" >break</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2021/11/05/python-break%e3%80%81continue%e3%80%81pass%e3%80%81return%e5%8f%8aexit%e7%9a%84%e7%94%a8%e6%b3%95%e8%88%87%e5%8d%80%e5%88%a5/#continue" >continue</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2021/11/05/python-break%e3%80%81continue%e3%80%81pass%e3%80%81return%e5%8f%8aexit%e7%9a%84%e7%94%a8%e6%b3%95%e8%88%87%e5%8d%80%e5%88%a5/#pass" >pass</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2021/11/05/python-break%e3%80%81continue%e3%80%81pass%e3%80%81return%e5%8f%8aexit%e7%9a%84%e7%94%a8%e6%b3%95%e8%88%87%e5%8d%80%e5%88%a5/#return" >return</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-5" href="https://quietbo.com/2021/11/05/python-break%e3%80%81continue%e3%80%81pass%e3%80%81return%e5%8f%8aexit%e7%9a%84%e7%94%a8%e6%b3%95%e8%88%87%e5%8d%80%e5%88%a5/#exit" >exit</a>
    </li>
  </ul></nav>
</div>

## <span class="ez-toc-section" id="break"></span>break<span class="ez-toc-section-end"></span> {.wp-block-heading}

用來終止循環語句，即使循環條件沒有False或者序列還沒被完全遞歸完，也會停止執行循環語句。

break語句用在while和for循環中。

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">def config():
    for num in '12345':
        if num == '3':
            break
        print('當前數字:', num)
    print('=' * 10)

config()</code></pre>

結果如下：

<pre class="wp-block-code"><code class="">當前數字: 1
當前數字: 2
==========</code></pre>



## <span class="ez-toc-section" id="continue"></span>continue<span class="ez-toc-section-end"></span> {.wp-block-heading}

continue 語句跳出**本次**循環，然後繼續進行下一輪循環。



<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">def config():
    for num in '12345':
        if num == '3':
            continue
        print('當前數字:', num)
    print('=' * 10)

config()</code></pre>

輸出結果：當for迴圈到3時，被跳過了。

<pre class="wp-block-code"><code class="">當前數字: 1
當前數字: 2
當前數字: 4
當前數字: 5
==========</code></pre>



## <span class="ez-toc-section" id="pass"></span>pass<span class="ez-toc-section-end"></span> {.wp-block-heading}

空語句，pass 不做任何事情，一般用做佔位語句，是為了保持程序結構的完整性。

<pre class="wp-block-code"><code lang="python" class="language-python">def config():
    for num in '12345':
        if num == '3':
            pass
        print('當前數字:', num)
    print('=' * 10)

config()</code></pre>

結果如下：

<pre class="wp-block-code"><code class="">當前數字: 1
當前數字: 2
當前數字: 3
當前數字: 4
當前數字: 5
==========</code></pre>

補充：

<blockquote class="wp-block-quote is-layout-flow wp-block-quote-is-layout-flow">
  <p>
    為什麼要站位？
  </p>
</blockquote>

<pre class="wp-block-code"><code class="">事實上站位就是要先預留位置，回頭再補上具體的代碼實現。
很多時候我們在開發的時候，會把已知的判斷條件或函式寫好，然後在對應的塊中寫上pass，後續再慢慢完善這些站位的部分。</code></pre>



## <span class="ez-toc-section" id="return"></span>return<span class="ez-toc-section-end"></span> {.wp-block-heading}

return 語句就是將結果返回到調用的地方，並把控制權也一起返回。



<pre class="wp-block-code"><code lang="python" class="language-python">def config():
    for num in '12345':
        if num == '3':
            return f'for迴圈在 {num} 時回傳了'
        print('當前數字:', num)
    print('=' * 10)

print(config())
print('上方function已返回')</code></pre>

結果如下：

<pre class="wp-block-code"><code class="">當前數字: 1
當前數字: 2
for迴圈在 3 時回傳了
上方function已返回</code></pre>



## <span class="ez-toc-section" id="exit"></span>exit<span class="ez-toc-section-end"></span> {.wp-block-heading}

用來結束整個程序（進程）。

<pre class="wp-block-code"><code lang="python" class="language-python">def config():
    for num in '12345':
        if num == '3':
            exit()
        print('當前數字:', num)
    print('=' * 10)

config()
print('*' * 10)  #程式已結束所以不會印出</code></pre>

顯示如下：

<pre class="wp-block-code"><code class="">當前數字: 1
當前數字: 2</code></pre>