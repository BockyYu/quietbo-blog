---
title: '[Linux] Makefile:8: *** missing separator. Stop.(已解決)'
author: Bocky
type: post
date: 2022-07-28T03:26:38+00:00
url: /2022/07/28/linux-makefile8-missing-separator-stop-已解決/
categories:
  - Linux
  - 系統相關
tags:
  - linux
  - makefile

---
原因:

出現這個錯誤的原因通常是tab格式錯誤導致的。Makefile的命令行必須以一個tab作為開頭, 不可用4個空白。

在~/.vimrc文件中添加：

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">set tabstop=4   //設置tab鍵是4個空格
set noexpandtab  //不把tab键用空格代替</code></pre>

查看目前的Makefile是否有tab鍵

<pre class="wp-block-code"><code lang="bash" class="language-bash">cat -t Makefile</code></pre>

當你看到`^I`代表tab。出問題的命令行如果前面是有空白, 代表該命令的指令是需要修改的