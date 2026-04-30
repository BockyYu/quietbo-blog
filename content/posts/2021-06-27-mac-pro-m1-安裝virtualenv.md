---
title: '[安裝]Mac pro M1 安裝virtualenv'
author: Bocky
type: post
date: 2021-06-27T11:55:45+00:00
url: /2021/06/27/mac-pro-m1-安裝virtualenv/
categories:
  - Python
tags:
  - 安裝

---
目前自帶版本有:  
Python 2.7.16  
Python 3.8.2

查詢路徑：

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">which python3  # which python</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/cjtmWq2.png" alt="" /> </figure> 

<ol class="wp-block-list">
  <li>
    安裝virtualenv<br />用pip就可以安裝 virtualenv，可以同時用在 Python 2 和 3，
  </li>
</ol>

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">pip install virtualenv</code></pre>

<ol class="wp-block-list" start="2">
  <li>
    創建虛擬環境
  </li>
</ol>

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">mkdir work_venv # 建立一個名為work_venv的資料夾
python3 -m virtualenv XXXvenv # 創建名為XXvenv的虛擬機</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/PXPLVuo.png" alt="" /> </figure> 

<ol class="wp-block-list" start="3">
  <li>
    進入/安裝模組/離開虛擬環境
  </li>
</ol>

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">source XXvenv/bin/activate

# 進到虛擬環境，最前面就會多（XXvenv）
pip list</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/unecAMW.png" alt="" /> </figure> 

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">pip install XXXX # 安裝模組
pip install -r requirements.txt  # 導入requirements.txt(路徑自行填寫)
deactivate # 離開虛擬環境</code></pre>