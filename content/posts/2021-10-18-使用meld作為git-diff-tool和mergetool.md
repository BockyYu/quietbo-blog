---
title: '[Git]使用Meld作為git diff tool'
author: Bocky
type: post
date: 2021-10-18T10:52:18+00:00
url: /2021/10/18/使用meld作為git-diff-tool和mergetool/
categories:
  - Git
tags:
  - GIT

---
環境:ubuntu20.04



<ol class="wp-block-list">
  <li>
    下載meld
  </li>
</ol>

<pre class="wp-block-code"><code class="">sudo apt-get install meld</code></pre>

<ol class="wp-block-list" start="2">
  <li>
    設置git
  </li>
</ol>

<pre class="wp-block-code"><code class="">git config --global diff.external meld </code></pre>

<ol class="wp-block-list" start="3">
  <li>
    在自己的的目錄下建立一個git-meld.sh 的script:
  </li>
</ol>

<pre class="wp-block-code"><code class="">vi ~/git-meld.sh </code></pre>

輸入:

<pre class="wp-block-code"><code class="">#!/bin/sh
meld $2 $5</code></pre>

<ol class="wp-block-list" start="4">
  <li>
    查看是否有存入
  </li>
</ol>

<pre class="wp-block-code"><code class="">cat ~/git-meld.sh</code></pre>

<ol class="wp-block-list" start="5">
  <li>
    改變檔案的屬性:
  </li>
</ol>

<pre class="wp-block-code"><code class="">chmod 777 ~/git-meld.sh</code></pre>

<ol class="wp-block-list" start="6">
  <li>
    把external diff 改成這個shell script:
  </li>
</ol>

<pre class="wp-block-code"><code class="">git config --global diff.external ~/git-meld.sh</code></pre>

<ol class="wp-block-list" start="7">
  <li>
    使用git diff
  </li>
</ol>

<pre class="wp-block-code"><code class="">git log # 複製選取要查看的commit_id
git diff [commit_id]</code></pre>