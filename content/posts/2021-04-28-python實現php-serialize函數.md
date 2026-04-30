---
title: '[Python]實現php serialize函數'
author: Bocky
type: post
date: 2021-04-28T08:50:46+00:00
url: /2021/04/28/python實現php-serialize函數/
categories:
  - Python
  - 程式語言
tags:
  - python

---
不同的程式語言之間物件的傳遞，就必須把物件序列化為標準格式，比如XML，但更好的方法是序列化為JSON，因為JSON表示出來就是一個字串，可以被所有語言讀取，也可以方便地儲存到磁碟或者通過網路傳輸。

舉例A公司用php撰寫後序列化(物件轉字串)傳送到B公司，而B公司用Python反序列化時要用到。  
通常是用在Python編程環境和PHP編程環境，相互之間需要`進行數據交換`時。<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/NTe1vwR.png" alt="" /> </figure> 

<pre class="wp-block-code"><code lang="bash" class="language-bash">pip3 install phpserialize</code></pre>

導入庫：

<pre class="wp-block-code"><code lang="bash" class="language-bash">import phpserialize</code></pre>

利用dumps 進行序列化（物件轉字串）：

<pre class="wp-block-code"><code lang="bash" class="language-bash">phpserialize.dumps(vary)</code></pre>

使用loads 進行反序列化（字串轉物件）：

<pre class="wp-block-code"><code lang="bash" class="language-bash">phpserialize.loads(formated_string)</code></pre>

[來源1][1]

 [1]: https://blog.csdn.net/whatday/article/details/106987049