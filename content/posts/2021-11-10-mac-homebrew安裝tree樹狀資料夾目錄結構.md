---
title: '[Mac] Homebrew安裝tree(樹狀資料夾目錄結構)'
author: Bocky
type: post
date: 2021-11-09T16:37:03+00:00
url: /2021/11/10/mac-homebrew安裝tree樹狀資料夾目錄結構/
categories:
  - 系統相關
tags:
  - m1

---
目的：使用homebrew來安裝tree，並顯示資料結構。  
<img decoding="async" src="https://i.imgur.com/P7VqLcb.png" alt="" /> 

## Homebrew {.wp-block-heading}

可以在 Mac 上安裝系統沒有的套件，例如 Wget (算是工程師滿常使用的軟體)

開啟終端機，輸入下方指令來安裝[Homebrew][1]

<pre class="wp-block-code"><code lang="bash" class="language-bash">/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"</code></pre>

更新套件

<pre class="wp-block-code"><code class="">brew update && brew upgrade && brew cleanup</code></pre>

安裝tree

<pre class="wp-block-code"><code class="">brew install tree</code></pre>

若在顯示列印資料夾目錄，中文檔名有亂碼時，加上 -N

<pre class="wp-block-code"><code class="">tree -N</code></pre>

有些資料夾層級太多時，可指定要印出的層數，後面加上層數的數字：

<pre class="wp-block-code"><code class="">tree -L 1</code></pre>

依字母排序

<pre class="wp-block-code"><code class="">tree -v</code></pre>

關鍵字搜尋 Homebrew 套件(下方是搜尋tree)

<pre class="wp-block-code"><code class="">brew search tree</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/VGyBRyQ.png" alt="" /> </figure> 

查看更多tree的功能：

<pre class="wp-block-code"><code class="">tree --help</code></pre>

 [1]: https://brew.sh/index_zh-tw.html