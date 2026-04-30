---
title: '[Python] grequest 出現 Monkey-patching ssl after ssl has already been imported may lead to errors, including RecursionError on Python 3.6. It may also silently lead to incorrect behaviour on Python 3.7. Please monkey-patch earlier(已解決)'
author: Bocky
type: post
date: 2023-05-02T14:56:10+00:00
url: /2023/05/02/python-grequest-出現-monkey-patching-ssl-after-ssl-has-already-been-imported-may-lead-to-errors-including-recursionerror-on-python-3-6-it-may-also-silently-lead-to-incorrect-behaviou/
categories:
  - Python

---
剛開始使用grequest就遇到這個Error，用這段訊息去找也沒有解決方式，一開始google到的都是要加下方這段，但仍然沒有解決根本的問題!

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">import gevent
from gevent import monkey
monkey.patch_all(select=False)</code></pre>

但我使用下方code，開啟一個新的py檔案就正常運行

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">import grequests

req_list = [   # 请求列表
    grequests.get('http://httpbin.org/get?a=1&b=2'),
    grequests.post('http://httpbin.org/post', data={'a':1,'b':2}),
    grequests.put('http://httpbin.org/post', json={'a': 1, 'b': 2}),
]

res_list = grequests.map(req_list)    # 并行发送，等最后一个运行完后返回
print(res_list[0].text)  # 打印第一个请求的响应文本</code></pre>

看一下[grequests的GitHub][1]  
最下面方有個最好的寫法<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/TSt5RhX.png" alt="" /> </figure> 

後來發現原本py檔有from其他py檔是有使用request的，把request前面import grequests就成功解決這個問題

 [1]: https://github.com/spyoungtech/grequests