---
title: '[SQL] 萬用字元與escape的用法(必知)'
author: Bocky
type: post
date: 2021-12-10T08:27:31+00:00
url: /2021/12/10/sql-萬用字元與escape的用法/
categories:
  - MySQL
tags:
  - SQL

---
<div id="ez-toc-container" class="ez-toc-v2_0_82_2 ez-toc-wrap-center counter-hierarchy ez-toc-counter ez-toc-grey ez-toc-container-direction">
  <div class="ez-toc-title-container">
    <p class="ez-toc-title" style="cursor:inherit">
      Table of Contents
    </p>
    
    <span class="ez-toc-title-toggle"><a href="#" class="ez-toc-pull-right ez-toc-btn ez-toc-btn-xs ez-toc-btn-default ez-toc-toggle" aria-label="顯示/隱藏內容目錄"><span class="ez-toc-js-icon-con"><span class=""><span class="eztoc-hide" style="display:none;">Toggle</span><span class="ez-toc-icon-toggle-span"><svg style="fill: #999;color:#999" xmlns="http://www.w3.org/2000/svg" class="list-377408" width="20px" height="20px" viewBox="0 0 24 24" fill="none"><path d="M6 6H4v2h2V6zm14 0H8v2h12V6zM4 11h2v2H4v-2zm16 0H8v2h12v-2zM4 16h2v2H4v-2zm16 0H8v2h12v-2z" fill="currentColor"></path></svg><svg style="fill: #999;color:#999" class="arrow-unsorted-368013" xmlns="http://www.w3.org/2000/svg" width="10px" height="10px" viewBox="0 0 24 24" version="1.2" baseProfile="tiny"><path d="M18.2 9.3l-6.2-6.3-6.2 6.3c-.2.2-.3.4-.3.7s.1.5.3.7c.2.2.4.3.7.3h11c.3 0 .5-.1.7-.3.2-.2.3-.5.3-.7s-.1-.5-.3-.7zM5.8 14.7l6.2 6.3 6.2-6.3c.2-.2.3-.5.3-.7s-.1-.5-.3-.7c-.2-.2-.4-.3-.7-.3h-11c-.3 0-.5.1-.7.3-.2.2-.3.5-.3.7s.1.5.3.7z"/></svg></span></span></span></a></span>
  </div><nav>
  
  <ul class='ez-toc-list ez-toc-list-level-1 ' >
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2021/12/10/sql-%e8%90%ac%e7%94%a8%e5%ad%97%e5%85%83%e8%88%87escape%e7%9a%84%e7%94%a8%e6%b3%95/#%E8%90%AC%E7%94%A8%E5%AD%97%E5%85%83%E7%94%A8%E6%B3%95" >萬用字元用法</a><ul class='ez-toc-list-level-3' >
        <li class='ez-toc-heading-level-3'>
          <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2021/12/10/sql-%e8%90%ac%e7%94%a8%e5%ad%97%e5%85%83%e8%88%87escape%e7%9a%84%e7%94%a8%e6%b3%95/#%E3%80%81%E3%80%81%E5%8F%8A1%E7%9A%84%E5%9B%9B%E7%A8%AE%E7%AF%84%E4%BE%8B" >[、]、[]及[1]的四種範例:</a>
        </li>
        <li class='ez-toc-page-1 ez-toc-heading-level-3'>
          <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2021/12/10/sql-%e8%90%ac%e7%94%a8%e5%ad%97%e5%85%83%e8%88%87escape%e7%9a%84%e7%94%a8%e6%b3%95/#%E4%BD%BF%E7%94%A8_like_%E5%8C%B9%E9%85%8D%E7%89%B9%E6%AE%8A%E5%AD%97%E5%85%83" >使用 like [] 匹配特殊字元</a>
        </li>
      </ul>
    </li>
    
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2021/12/10/sql-%e8%90%ac%e7%94%a8%e5%ad%97%e5%85%83%e8%88%87escape%e7%9a%84%e7%94%a8%e6%b3%95/#escape%E7%9A%84%E7%94%A8%E6%B3%95" >escape的用法</a>
    </li>
  </ul></nav>
</div>

## <span class="ez-toc-section" id="%E8%90%AC%E7%94%A8%E5%AD%97%E5%85%83%E7%94%A8%E6%B3%95"></span>萬用字元用法<span class="ez-toc-section-end"></span> {.wp-block-heading}

<ul class="wp-block-list">
  <li>
    %：匹配零個及多個任意字元
  </li>
  <li>
    _ <em>：與任意1個單字元匹配，包含</em>
  </li>
  <li>
    []：匹配一個範圍
  </li>
  <li>
    [^]：排除一個範圍
  </li>
</ul>

字串中出現的特殊字元：`%<strong> [ [] _</strong>` 

可以使用 &#8216;[]&#8217; 把特殊字元包起來，這些特殊字元就被當作普通字元對待了。

### <span class="ez-toc-section" id="%E3%80%81%E3%80%81%E5%8F%8A1%E7%9A%84%E5%9B%9B%E7%A8%AE%E7%AF%84%E4%BE%8B"></span>[、]、[]及[1]的四種範例:<span class="ez-toc-section-end"></span> {.wp-block-heading}

以下SQL使用 like [] 匹配特殊字元 [ 與 []

<pre class="wp-block-code"><code lang="sql" class="language-sql line-numbers">-- 使用[[]
select 1 where '[TEST' like '[[]%'; -- 1
select 1 where 'TEST[' like '%[[]'; -- 1

-- 這邊的]是不需要包起來，只需要寫在like內即可
select 1 where 'TEST]' like '%]'; -- 1
select 1 where ']TEST' like ']%'; -- 1

-- 使用[[]]
select 1 where '[]TEST' like '[[]]%%'; -- 1

-- 稍微複雜一點包法，前面的[1]要用[[]1]包
select 1 where '[1]TEST' like '[[]1]%%'; -- 1</code></pre>

### <span class="ez-toc-section" id="%E4%BD%BF%E7%94%A8_like_%E5%8C%B9%E9%85%8D%E7%89%B9%E6%AE%8A%E5%AD%97%E5%85%83"></span>使用 like [_] 匹配特殊字元_<span class="ez-toc-section-end"></span> {.wp-block-heading}

原本 _ 的功能是與任意單字元匹配，  
如果想搜尋是DB\_開頭的話，使用單純的\_又會把DBa、DBb什麼db開頭的家人都找出來，變模糊搜尋了。

<pre class="wp-block-code"><code lang="sql" class="language-sql line-numbers">--原本:
select 1 where 'DB_' like '___'; -- 1
select 1 where 'DBa' like '___'; -- 1
select 1 where 'DBb' like '___'; -- 1</code></pre>

如果確定只要DB\_開頭，就必須把\_用[]包起來，這樣其他的就找不到了!

<pre class="wp-block-code"><code lang="sql" class="language-sql">select 1 where 'DBatest' like 'db[_]%'; -- 無
select 1 where 'DBbtest' like 'db[_]%'; -- 無
select 1 where 'DB_test' like 'db[_]%'; -- 1</code></pre>

## <span class="ez-toc-section" id="escape%E7%9A%84%E7%94%A8%E6%B3%95"></span>escape的用法<span class="ez-toc-section-end"></span> {.wp-block-heading}

escape要與Like一起使用，定義轉義符  
若不使用[]包住%，來搜尋&#8217;10%&#8217;，也許會很直覺的使用`like '10%'`  
但這樣會把100%、101%、1000%等10開頭都搜尋到，與預期結果不符。

<pre class="wp-block-code"><code lang="sql" class="language-sql line-numbers">SELECT 1 WHERE '100%' LIKE '10%'; -- 1
SELECT 1 WHERE '101%' LIKE '10%'; -- 1
SELECT 1 WHERE '102%' LIKE '10%'; -- 1
SELECT 1 WHERE '10000%' LIKE '10%'; -- 1</code></pre>

下方指令是使用escape來尋找真正的%

<pre class="wp-block-code"><code lang="sql" class="language-sql line-numbers"> SELECT 1 WHERE '10%' LIKE '10/%'  ESCAPE '/'  ;</code></pre>

上方的是指定用&#8217;/&#8217;符號來說明，後面的萬用符轉成普通字符(單純的百分比%)，  
如果同時要尋找/的話呢?例如日期常使用到的/  
一般沒有使用ESCAPE的話，可能直接打上日期(下方第一個)搜尋，  
若加入 ESCAPE &#8216;/&#8217; ，要使用2個/，這樣才能符合。

<pre class="wp-block-code"><code lang="sql" class="language-sql line-numbers">SELECT 1 WHERE '2021/12/31' LIKE '2021/12/31'; -- 1
SELECT 1 WHERE '2021/12/31' LIKE '2021//12//31'  ESCAPE '/'; -- 1
SELECT 1 WHERE 'MSSQL/50%' LIKE 'MSSQL/50%'  ESCAPE '/'; -- 0
SELECT 1 WHERE 'MSSQL/50%' LIKE 'MSSQL//50/%'  ESCAPE '/'; -- 1</code></pre>