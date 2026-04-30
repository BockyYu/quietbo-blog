---
title: '[Ubuntu] Terminator+ZSH'
author: Bocky
type: post
date: 2022-07-16T16:26:36+00:00
url: /2022/07/17/ubuntu-terminatorzsh/
categories:
  - 系統相關
tags:
  - ubuntu

---
多窗口如下:  
<img decoding="async" src="https://i.imgur.com/T32W7Qv.png" alt="" /> 

## Terminator {.wp-block-heading}

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">$ #sudo add-apt-repository ppa:gnome-terminator
$ sudo apt update
$ sudo apt install terminator</code></pre>

## zsh {.wp-block-heading}

更新apt-get

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">$sudo apt-get update
$sudo apt-get upgrade</code></pre>

安裝 zsh

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">$sudo apt-get install zsh</code></pre>

安裝git

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">$sudo apt-get install git</code></pre>

查看一下是否安裝成功

<pre class="wp-block-code"><code class="">$cat /etc/shells

# /etc/shells: valid login shells
/bin/sh
/bin/bash
/usr/bin/bash
/bin/rbash
/usr/bin/rbash
/bin/dash
/usr/bin/dash
/bin/zsh
/usr/bin/zsh</code></pre>

安裝 curl

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ sudo apt-get install curl</code></pre>

安裝 oh-my-zsh

<pre class="wp-block-code"><code lang="bash" class="language-bash">$sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"</code></pre>

修改配置

<pre class="wp-block-code"><code lang="bash" class="language-bash">$chsh -s /bin/zsh</code></pre>

官方主題庫:[Github網址][1]

 [1]: https://github.com/ohmyzsh/ohmyzsh/wiki/External-themes