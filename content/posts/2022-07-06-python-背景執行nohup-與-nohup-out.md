---
title: '[Python] 背景執行nohup, & 與 nohup.out'
author: Bocky
type: post
date: 2022-07-06T10:13:54+00:00
url: /2022/07/06/python-背景執行nohup-與-nohup-out/
categories:
  - Python
  - 系統相關
tags:
  - python

---
#  {.wp-block-heading}

本篇提到的「**背景**」指的是: 在終端機模式下使用 [ctrl]-c, 並不會中斷的一個情境!

<a href="https://quietbo.com/2021/03/10/ubuntu%e8%83%8c%e6%99%af%e5%9f%b7%e8%a1%8cpy%e6%96%b9%e6%b3%95/" target="_blank" rel="noreferrer noopener">[Linux]背景執行py方法</a> 雖然是在背景執行, 不會因為[ctrl]-c而中斷, 但會因為「**終端機關閉後而中斷**」。

<p id="block-b1f3c7ea-6b97-4897-bb83-e416e7bdabac">
  中斷可能多個原因, 例如ssh連線到機器後, 操作時不小心將視窗關閉,或是網路斷線而關閉。
</p>

本次主要目的為: 「**在離線或登出系統後，還能夠讓工作繼續進行**」。

演示的code為my_nohup.py:

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers"># coding:utf-8
from datetime import datetime
from time import sleep
import logging

Log_Format = "%(levelname)s %(asctime)s - %(message)s"

logging.basicConfig(filename = "mylog.log",
                    filemode = "w",
                    format = Log_Format,
                    level = logging.INFO)
logger = logging.getLogger()
logger.error("Our First Log Message")

while(1):
    sleep(5)

    print("print " + str(datetime.now().strftime('%Y-%m-%d %H:%M:%S')))
    logger.info(str(datetime.now().strftime('%Y-%m-%d %H:%M:%S')))
    # print(1/0) # 輸出錯誤時使用</code></pre>

# <span class="ez-toc-section" id="%E6%8C%87%E4%BB%A4%E4%BB%8B%E7%B4%B9"></span>指令介紹<span class="ez-toc-section-end"></span> {.wp-block-heading}

<ul class="wp-block-list">
  <li>
    <code>nohup</code>: no hang up的縮寫, 不斷地運行。
  </li>
  <li>
    <code>&</code>: 在後台運行，關掉終端會停止運行。
  </li>
  <li>
    <code>&gt;</code> : 標準輸出符號。
  </li>
  <li>
    <code>-u</code>: 在nohup.out內可以看到print的訊息。
  </li>
</ul>

## <span class="ez-toc-section" id="%E8%83%8C%E6%99%AF%E5%9F%B7%E8%A1%8Cnohup"></span>背景執行(nohup, &)<span class="ez-toc-section-end"></span> {.wp-block-heading}

<pre class="wp-block-code"><code lang="bash" class="language-bash">nohup python3 my_nohup.py &</code></pre>

758865 為背景執行的PID  
<img decoding="async" src="https://i.imgur.com/Ixd9tqD.png" alt="" /> 

執行完會出現一段，所有輸出都被重定向到一個名為nohup.out的文件中

<pre class="wp-block-code"><code class="">nohup: ignoring input and appending output to 'nohup.out'</code></pre>

此時輸入ls指令會看到多出mylog.log和nohup.out

<pre class="wp-block-code"><code lang="bash" class="language-bash">admins@labs:~$ ls
Dev  get-pip.py  mylog.log  my_nohup.py  nohup.out  Python-3.7.9</code></pre>

試著使用cat去看看這兩隻檔案, mylog.log會每5秒打印訊息, 但nohup.out是空的。

查看背景運行(若是關閉終端機後才使用指令，jobs已經無法看到後台跑得程序了, 需使用ps aux)

<pre class="wp-block-code"><code lang="bash" class="language-bash">jobs -l</code></pre>

離開該終端機後, 背景仍會繼續執行這個服務, 可使用ps aux來查看。

## <span class="ez-toc-section" id="%E8%A7%A3%E6%B1%BA_nohupout%E6%89%93%E9%96%8B%E6%98%AF%E7%A9%BA%E7%99%BD%E5%95%8F%E9%A1%8C"></span>[解決] nohup.out打開是空白問題<span class="ez-toc-section-end"></span> {.wp-block-heading}

如果沒有指定導出的地方, 會在nohup.out檔案內, 但在執行時需使用  
python -u  
執行時使用下方指令:

<pre class="wp-block-code"><code class="">nohup python3 -u my_nohup.py &</code></pre>

這樣print內的訊息都會在nohup.out了, 而log則是logger寫入的資料, 是分開的檔案。

## <span class="ez-toc-section" id="%E6%8C%87%E5%AE%9A%E8%BC%B8%E5%87%BA%E6%AA%94%E6%A1%88%E5%B0%8E%E5%87%BA%E6%AA%94%E6%A1%88"></span>指定輸出檔案(導出檔案)<span class="ez-toc-section-end"></span> {.wp-block-heading}

可以指定導到其他檔案, 下方是導到my_print.txt

<pre class="wp-block-code"><code class="">nohup python3 -u my_nohup.py &gt; my_print.txt &</code></pre>

沒有nohup: ignoring input and appending output to &#8216;nohup.out&#8217;的訊息, 也沒有看到nohup.out的檔案。  
<img decoding="async" src="https://i.imgur.com/cg3xS8W.png" alt="" /> 

這裡的>其實是 1> 的縮寫。<figure class="wp-block-table">

| 名稱     | 代碼 | 操作符號         |
| ------ | -- | ------------ |
| 標準輸入   |    | < 或<<        |
| 標準輸出   | 1  | >或>>或1> 或1>> |
| 標準錯誤輸出 | 2  | 2> 或2>>      |</figure> 

通常後台運行重定向可以寫成：

<pre class="wp-block-code"><code class="">mkdir logs
nohup python3 -u my_nohup.py &gt; logs/command.log 2&gt;&1 &</code></pre>

2>&1 是將「標準錯誤輸出(2)」重定向到「標準輸出(1)」, 簡單來說就是**標準輸出和標準錯誤輸出都在同一份檔案**, 導入logs文件夾下的command.log日誌文件。

## <span class="ez-toc-section" id="%E6%A8%99%E6%BA%96%E8%BC%B8%E5%87%BA%E8%88%87%E6%A8%99%E6%BA%96%E9%8C%AF%E8%AA%A4%E8%BC%B8%E5%87%BA%E5%88%86%E9%96%8B%E5%84%B2%E5%AD%98"></span>標準輸出與標準錯誤輸出分開儲存<span class="ez-toc-section-end"></span> {.wp-block-heading}

如果想要把錯誤輸出存到另一份檔案,把最後一行的註解拿掉， print(1/0)在最後運行時會出錯, 下方指令, 會把標準輸出到out.log, 標準錯誤輸出err.log

<pre class="wp-block-code"><code class="">nohup python3 -u my_nohup.py &gt; out.log 2&gt;err.log &</code></pre>

下方為故意讓程式有出錯的狀況的圖片, 會看到out.log是原本的print日期時間, 而err.log則是遇到錯誤的訊息  
<img decoding="async" src="https://i.imgur.com/mMogv4p.png" alt="" /> 

<hr class="wp-block-separator has-alpha-channel-opacity" />

補充:  
<a href="https://linux.vbird.org/linux_basic/centos7/0440processcontrol.php#nohup" target="_blank" rel="noreferrer noopener">鳥哥私房菜-離線管理問題</a>