---
title: '[Python] 製作一個exe檔案在windows執行'
author: Bocky
type: post
date: 2022-12-11T08:03:13+00:00
url: /2022/12/11/python-製作一個exe檔案在windows執行/
categories:
  - Python

---
<ul class="wp-block-list">
  <li>
    Windows 11
  </li>
  <li>
    IDE:PyCharm 2022.3 (Community Edition)
  </li>
  <li>
    Python3.7
  </li>
  <li>
    package:PyInstaller
  </li>
</ul>

以下為pycharm初始的Code，請先確認環境與package可install與執行指令。

本篇程式碼檔案名為main.py

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers"># This is a sample Python script.

# Press Shift+F10 to execute it or replace it with your code.
# Press Double Shift to search everywhere for classes, files, tool windows, actions, and settings.


def print_hi(name):
    # Use a breakpoint in the code line below to debug your script.
    print(f'Hi, {name}')  # Press Ctrl+F8 to toggle the breakpoint.


# Press the green button in the gutter to run the script.
if __name__ == '__main__':
    print_hi('PyCharm')

# See PyCharm help at https://www.jetbrains.com/help/pycharm/</code></pre>

安裝:

<pre class="wp-block-code"><code class="">pip install pyinstaller</code></pre>

執行下方指令

<pre class="wp-block-code"><code class="">pyinstaller -F .\{檔案名稱}.py</code></pre>

範例:

<pre class="wp-block-code"><code class="">pyinstaller -F .\main.py</code></pre>

執行會出現一大串訊息，本篇只擷取部分畫面:  
<img decoding="async" src="https://i.imgur.com/RF0ZDaJ.png" alt="" /> 

開啟資料夾查看  
<img decoding="async" src="https://i.imgur.com/wclI2Ox.png" alt="" /> 

會建立以下

<ul class="wp-block-list">
  <li>
    main.spec
  </li>
  <li>
    build 資料夾 (log與工作檔案)
  </li>
  <li>
    dist 資料夾(要執行的exe檔案在這裡面)
  </li>
</ul>

打開dist會看到main.exe，點擊後會馬上出現命令提示字元後馬上又消失。  
如果想要暫停住的話可加入input()在Code內。<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/rrvkrP2.png" alt="" /> </figure> 

再重新pyinstaller -F .\main.py一次，重新點擊main.exe即可停留在下方畫面。  
<img decoding="async" src="https://i.imgur.com/vmbVcrL.png" alt="" />