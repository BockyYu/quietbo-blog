---
title: '[Python] os.chdir 更改當前工作目錄'
author: Bocky
type: post
date: 2022-07-19T09:49:44+00:00
url: /2022/07/19/python-os-chdir-更改當前工作目錄/
categories:
  - Python
tags:
  - python

---
語法:

<pre class="wp-block-code"><code lang="basic" class="language-basic">os.chdir(path)</code></pre>

參數

<ul class="wp-block-list">
  <li>
    path − 更改到新位置的目錄的完整路徑。
  </li>
</ul>

不返回任何值。沒有找到指定的路徑，會拋出FileNotFoundError

舉例:  
我在跟目錄(/)的狀態下, 使用python3 絕對路徑/xxxx.py後, 要在運行別隻py檔案,

使用下方兩隻py檔來做演示,路徑都在/home/ubuntu/Dev

檔名:chdir.py

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">#!/usr/bin/python
# -*- coding: UTF-8 -*-

import os, sys

path = "/home/ubuntu/Dev"

# 查看當前工作目錄
retval = os.getcwd()
print("當前工作目錄:%s" % retval)

# 修改當前工作目錄
os.chdir( path )

# 查看修改後的工作目錄
retval = os.getcwd()

print("目錄修改成功:%s" % retval)

# 接著要運行的指令
os.system("python3 pping.py") </code></pre>

檔名:pping.py

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">import os
a=os.system("ping 192.168.1.101")  #使用a接收返回值
print(a)</code></pre>

以下是在終端機執行過程:

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">ubuntu@ubuntu:~/Dev$ cd ~
ubuntu@ubuntu:~$ python3 /home/ubuntu/Dev/chdir.py 
當前工作目錄:/home/ubuntu
目錄修改成功:/home/ubuntu/Dev
PING 192.168.1.101 (192.168.1.101) 56(84) bytes of data.
64 bytes from 192.168.1.101: icmp_seq=1 ttl=128 time=5.19 ms</code></pre>

由此可見os.getcwd是獲得終端機當下在運行python時的路徑, 而os.chdir是會修改為新的工作路徑, 若沒有修改的話, 是沒辦法透過os.system來運行pping.py的, 會出現找不到檔案的error。