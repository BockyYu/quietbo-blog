---
title: '[Python] 日誌記錄第三方庫 – Loguru(附簡單的範例)'
author: Bocky
type: post
date: 2022-08-12T11:01:01+00:00
url: /2022/08/12/python-日誌記錄第三方庫-loguru附簡單的範例/
categories:
  - Python
tags:
  - python

---
use:

<pre class="wp-block-code"><code class="">pycharm, FastAPI, Loguru</code></pre>

一開始在學log時, 會使用標準庫 logging。  
設置上較爲繁瑣, 甚至有些在多進程多線程等特殊處理時, 還會導致日誌記錄會出現異常, 還有幾次都在找為什麼logg會印兩次…  
現在單純開發時都會使用Loguru來做一些log的紀錄,下方提供簡單的範例

## 安裝 

使用 pip 安裝即可，Python 3 版本的安裝如下：

<pre class="wp-block-code"><code class="">pip3 install loguru</code></pre>

log.py

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">from loguru import logger
logger.add("./logs/test.log", rotation="00:00", enqueue=True, retention="30 days")

#logger.info(1)
#logger.error(2)
#logger.warning(3)</code></pre>

main.py

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">import uvicorn
from log import logger
from fastapi import FastAPI

app = FastAPI()

@app.on_event("startup")
async def startup_event():
    logger.info('Hi startup')

@app.get("/")
async def root():
    return {"message": "Hello World"}


if __name__ == "__main__":
    uvicorn.run("main:app", host='127.0.0.1', port=8000, reload=True)</code></pre>

執行python main.py

會看到下方的

<pre class="wp-block-code"><code lang="bash" class="language-bash">INFO:     Will watch for changes in these directories: ['C:\\Dev\\FastAPI_demo']
INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
INFO:     Started reloader process [21476] using watchgod
INFO:     Started server process [4168]
INFO:     Waiting for application startup.
2022-08-12 18:53:32.579 | INFO     | main:startup_event:9 - Hi startup
INFO:     Application startup complete.</code></pre>

打開瀏覽器輸入下方:

<pre class="wp-block-code"><code class="">127.0.0.1/</code></pre>

打開logs資料夾會看到已經有印出來的檔案。

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">2022-08-12 18:56:21.419 | INFO     | main:startup_event:9 - Hi startup
2022-08-12 18:56:27.969 | INFO     | main:root:13 - {'message': 'Hello World'}</code></pre>