---
title: '[Pycharm] 導出&導入虛擬環境(venv導出requirements)'
author: Bocky
type: post
date: 2022-04-06T05:24:22+00:00
url: /2022/04/06/pycharm-導出導入虛擬環境venv導出requirements/
categories:
  - Editor;IDE;GUI
  - Python
tags:
  - pycharm
  - python

---
 

## 導出虛擬環境 

一般命令為導出的是系統環境，不是虛擬環境(venv)

<pre class="wp-block-code"><code lang="bash" class="language-bash">pip freeze &gt; requirements.txt</code></pre>

在windows終端下是不可以使用的，使用以下代碼進行導出，運行後會產生requirements.txt

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">import os
import platform
import sys
import subprocess

# 當前目錄
project_root = os.path.dirname(os.path.realpath(__file__))
# project_root = os.path.realpath(__file__)
print('當前目錄' + project_root)

# 依據目前使用不同的系統會使用不同的command,目前使用linux及Windows
if platform.system() == 'Linux':
    command = sys.executable + ' -m pip freeze &gt; ' + project_root + '/requirements.txt'
if platform.system() == 'Windows':
    command = '"' + sys.executable + '"' + ' -m pip freeze &gt; "' + project_root + '\\requirements.txt"'
# 生成requirements的命令
print(command)
#
# 執行command
# os.system(command)  #路徑有空格時不可用
os.popen(command)  # 路徑有空格可用</code></pre>

## 安装requirement 

開啟新的專案想使用requirement時，打開終端機輸入:

<pre class="wp-block-code"><code lang="bash" class="language-bash">pip install -r requirement.txt</code></pre>