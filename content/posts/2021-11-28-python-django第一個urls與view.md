---
title: '[Python] Django第一個Urls與View'
author: Bocky
type: post
date: 2021-11-28T09:13:19+00:00
url: /2021/11/28/python-django第一個urls與view/
categories:
  - Python
tags:
  - python

---
<ol class="wp-block-list">
  <li>
    定義視圖函數<br />books\views.py:
  </li>
</ol>

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">from django.shortcuts import render
from django.http import HttpResponse

#定義視圖函數
def hello(request):
    return HttpResponse("&lt;h1&gt;Hello, world.世界你好.&lt;/h1&gt;")</code></pre>

<ol class="wp-block-list" start="2">
  <li>
    修改項目(mydjango) urls.py文件
  </li>
</ol>

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('books/', include('books.urls')),
    path('admin/', admin.site.urls),
]</code></pre>

<ol class="wp-block-list" start="3">
  <li>
    在books的資料夾新增 urls.py文件
  </li>
</ol>

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">from django.urls import path
from . import views

urlpatterns = [
    path('hello/', views.hello, name='hello'),
]</code></pre>

建立完成後的資料如下，執行

<pre class="wp-block-code"><code lang="bash" class="language-bash">python manage.py runserver</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/A4uX13g.png" alt="" /> </figure> <figure class="wp-block-image"><img decoding="async" src="https://i.imgur.com/gkEr4Ol.png" alt="" /></figure> 

開啟瀏覽器，輸入

<pre class="wp-block-code"><code class="">http://127.0.0.1:8000/books/hello/</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/cjoWs3K.png" alt="" /> </figure> 

## URL配置 {.wp-block-heading}

<ol class="wp-block-list">
  <li>
    urlpatterns: 路由模式列表,通過URL模式映射到視圖
  </li>
  <li>
    path函數： 返回urlpatterns元素<br />定義：path(route, view, kwargs=None, name=None)<br />route：路由模式,<br />view:可以是視圖函數、視圖類或include函數返回值<br />path(&#8221;, views.home, name=&#8217;home&#8217;)<br />path(&#8221;, Home.as_view(), name=&#8217;home&#8217;)<br />path(&#8216;blog/&#8217;, include(&#8216;blog.urls&#8217;))
  </li>
  <li>
    include函數：導入其他的模塊,include(&#8216;books.urls&#8217;)是導入books.urls模塊
  </li>
</ol>