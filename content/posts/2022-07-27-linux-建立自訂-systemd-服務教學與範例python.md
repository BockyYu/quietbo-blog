---
title: '[Linux]  建立自訂 Systemd 服務教學與範例(Python)'
author: Bocky
type: post
date: 2022-07-27T07:33:45+00:00
url: /2022/07/27/linux-建立自訂-systemd-服務教學與範例python/
categories:
  - Linux
  - 系統相關
tags:
  - linux
  - systemd

---
[Linux 建立自訂 Systemd 服務教學與範例][1]

# 部屬方式 

本次範例程式使用FastAPI,  
檔名為main.py

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">import platform
import os
os_type = platform.system()
if os_type == 'Linux':
    # print('in Linux')
    os.chdir('/home/ubuntu/Dev')
import sys
sys.path.append("/home/ubuntu/.local/lib/python3.8/site-packages")
from fastapi import FastAPI
import uvicorn


app = FastAPI()

@app.get("/")
async def root():
    return {"message": "Hello World"}

if __name__ == "__main__":
    uvicorn.run("main:app", host='0.0.0.0', port=8080, workers=1, reload=True)</code></pre>

# Linux 建立自訂 Systemd 服務教學與範例 

<ol class="wp-block-list">
  <li>
    到/etc建立或rc.local並輸入下列內容(如果沒有的話自行建立)
  </li>
</ol>

<ul class="wp-block-list">
  <li>
    更改檔案路徑
  </li>
  <li>
    python執行檔路徑, 有些是/bin/python, 請自行更改(若想包成docker就寫執行docker容器的指令)
  </li>
</ul>

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">#!/bin/sh -e

cd /home/ubuntu/Dev/myPython

/usr/bin/python3 main.py

exit 0</code></pre>

確定輸入的python路徑正確, 使程式正常運行:

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ /usr/bin/python3 data_collector_main.py</code></pre>

然後將執行權限添加到 /etc/rc.local 文件。

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ sudo chmod +x /etc/rc.local</code></pre>

<ol class="wp-block-list" start="2">
  <li>
    到/etc/systemd/system建立rc-local.service服務
  </li>
</ol>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ nano /etc/systemd/system/rc-local.service</code></pre>

如果是依照rc.local則直接複製下方內容,無須修正  
(有修改過rc.local檔名的話, 請自行將下方的4處修改為自己的檔名, 分別為下方的1,4,9,17行)

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">[Unit]
Description=/etc/rc.local Compatibility
Documentation=man:systemd-rc-local-generator(8)
ConditionFileIsExecutable=/etc/rc.local
After=network.target

[Service]
Type=forking
ExecStart=/etc/rc.local start
Environment="DJANGO_SETTINGS_MODULE=Macdonald_Server.settings.production"
TimeoutSec=0
RemainAfterExit=yes
GuessMainPID=no

[Install]
WantedBy=multi-user.target
Alias=rc-local.service</code></pre>

<ol class="wp-block-list" start="3">
  <li>
    python的庫位置
  </li>
</ol>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ pip3 show fastapi</code></pre>

<ol class="wp-block-list" start="4">
  <li>
    添加PATH, 路徑請自行更改
  </li>
</ol>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ export PATH=$PATH:/home/nadi_19/.local/lib/python3.6/site-packages</code></pre>

<ol class="wp-block-list" start="5">
  <li>
    開啟執行權限
  </li>
</ol>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ chmod +x /home/nadi_19/NADI/ShowCase/server_ms_showcase/data_collector/data_collector_main.py</code></pre>

<ol class="wp-block-list" start="6">
  <li>
    重新載入 Systemd 設定檔
  </li>
</ol>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ sudo systemctl daemon-reload</code></pre>

<ol class="wp-block-list" start="7">
  <li>
    啟動自訂的 echo 伺服器
  </li>
</ol>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ sudo systemctl start rc-local.service</code></pre>

<ol class="wp-block-list" start="8">
  <li>
    查看 echo 伺服器狀態
  </li>
</ol>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ sudo systemctl status rc-local.service</code></pre>

成功啟動訊息如下:

<pre class="wp-block-code"><code lang="bash" class="language-bash">root@ShowCase19-1:/home/nadi_19/NADI/ShowCase/server_ms_showcase/data_collector# systemctl status rc-local
● rc-local.service - /etc/rc.local Compatibility
   Loaded: loaded (/etc/systemd/system/rc-local.service; enabled; vendor preset: enabled)
  Drop-In: /lib/systemd/system/rc-local.service.d
           └─debian.conf
   Active: active (exited) since Wed 2022-07-20 11:15:40 UTC; 1min 27s ago
     Docs: man:systemd-rc-local-generator(8)
  Process: 31493 ExecStart=/etc/rc.local start (code=exited, status=0/SUCCESS)</code></pre>

<ol class="wp-block-list" start="9">
  <li>
    使服務能夠在啟動時自動啟動
  </li>
</ol>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ sudo systemctl enable rc-local.service</code></pre>

輸入完後重新開機, 測試看看是否service都有自己run起來!

<ol class="wp-block-list" start="10">
  <li>
    指令補充
  </li>
</ol>

下方的service-name都是指rc-local.service這隻檔案。

<ul class="wp-block-list">
  <li>
    檢視服務的當前狀態<br />無論它是否正在執行，都可以在終端中使用以下命令語法：
  </li>
</ul>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ systemctl status [service-name]</code></pre>

<ul class="wp-block-list">
  <li>
    啟動服務，請使用以下語法
  </li>
</ul>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ systemctl start [service-name]</code></pre>

<ul class="wp-block-list">
  <li>
    停止正在執行的服務
  </li>
</ul>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ systemctl stop [service-name]</code></pre>

<ul class="wp-block-list">
  <li>
    使服務能夠在機器啟動時自動啟動
  </li>
</ul>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ systemctl enable [service-name]</code></pre>

<ul class="wp-block-list">
  <li>
    禁用服務，使其無法在啟動時自動啟動：
  </li>
</ul>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ systemctl disable [service-name]</code></pre>

<ul class="wp-block-list">
  <li>
    重新載入服務
  </li>
</ul>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ systemctl reload [service-name]</code></pre>

<ul class="wp-block-list">
  <li>
    重新載入<br />或重新啟動服務（它重新載入服務，並且如果重新載入不可用，那麼它將重新啟動服務。）
  </li>
</ul>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ sudo systemctl reload-or-restart [service-name]</code></pre>

<ul class="wp-block-list">
  <li>
    檢查服務是否啟用
  </li>
</ul>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ sudo systemctl is-active [service-name]</code></pre>

服務正常並啟用則返回:activating

<ul class="wp-block-list">
  <li>
    檢查是否已啟用服務以在系統啟動時自動啟動
  </li>
</ul>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ sudo systemctl is-enabled [service-name]</code></pre>

啟用則返回:enabled

## 補充 

<ol class="wp-block-list">
  <li>
    若是出現Condition check resulted in /etc/rc.local Compatibility being skipped.
  </li>
</ol>

將執行權限添加到 /etc/rc.local 文件。

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ sudo chmod +x /etc/rc.local</code></pre>

<ol class="wp-block-list" start="2">
  <li>
    找不到xxx.local檔案<br />如果在確認etc是否有xxx.local,如果沒有的話請將自己補上, 或是.service檔案內的xx.local檔名打錯了。
  </li>
  <li>
    執行多個service<br />目前是建立多個xx.local和xx-local.service,<br />未來若有更好的方式, 我會來修正現在的方式(如果我有記得的話)
  </li>
</ol>

 [1]: https://blog.gtwang.org/linux/linux-create-systemd-service-unit-for-python-echo-server-tutorial-examples/