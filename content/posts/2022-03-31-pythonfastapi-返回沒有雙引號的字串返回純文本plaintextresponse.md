---
title: '[Python|FastAPI] 返回沒有雙引號的字串(返回純文本)PlainTextResponse'
author: Bocky
type: post
date: 2022-03-31T10:26:15+00:00
url: /2022/03/31/pythonfastapi-返回沒有雙引號的字串返回純文本plaintextresponse/
categories:
  - Python
tags:
  - FastAPI
  - python

---
問題:  
對方是要的訊息Hello World，不是要&#8221;Hello World&#8221;

原本的FastAPI寫法如下:

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">from fastapi import FastAPI
import uvicorn

app = FastAPI()


@app.get("/")
async def root():
    return "Hello World"

if __name__ == "__main__":
    uvicorn.run("main:app", host="127.0.0.1", port=8000)</code></pre><figure class="wp-block-image is-style-default">

<img decoding="async" src="https://i.imgur.com/f23g0hl.png" alt="" /> </figure> 

可以看到最常見的postman發的請求得到是&#8221;Hello World&#8221;

解決方式:  
使用:[PlainTextResponse][1]

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">from fastapi import FastAPI
import uvicorn
from fastapi.responses import PlainTextResponse

app = FastAPI()


@app.get("/", response_class=PlainTextResponse)
async def root():
    return "Hello World"

if __name__ == "__main__":
    uvicorn.run("main:app", host="127.0.0.1", port=8000)</code></pre><figure class="wp-block-image is-style-default">

<img decoding="async" src="https://i.imgur.com/VHdSY2i.png" alt="" /> </figure> 

可以看到還滿順利的出現了單純只有文字的Hello World

不一定要放在response_class，以下方式也能成功:

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">from fastapi import FastAPI
import uvicorn
from fastapi.responses import PlainTextResponse

app = FastAPI()

def get_text(parameters):
    text = PlainTextResponse(parameters)
    return text


@app.get("/")
async def root():
    op = get_text('hello bocky')
    return op

if __name__ == "__main__":
    uvicorn.run("main:app", host="127.0.0.1", port=8000)</code></pre><figure class="wp-block-image is-style-default">

<img decoding="async" src="https://i.imgur.com/VpbKCPd.png" alt="" /> </figure>

 [1]: https://fastapi.tiangolo.com/advanced/custom-response/#plaintextresponse