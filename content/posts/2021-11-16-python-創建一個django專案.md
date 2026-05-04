---
title: '[Python] 創建一個Django專案'
author: Bocky
type: post
date: 2021-11-15T16:08:12+00:00
url: /2021/11/16/python-創建一個django專案/
categories:
  - Python
tags:
  - Django
  - python

---
使用：Mac M1  
Python 3.8  
Django:3.2

## 建立環境 

可參考：[安裝virtualenv][1]

進入env後，安裝及查看Django版本：

<pre class="wp-block-code"><code class="">pip install django
pip list</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/YDA0rRK.png" alt="" /> </figure> 

## 建立專案 

尋找一個位置，建立第一個專案：

<pre class="wp-block-code"><code class="">django-admin startproject mydjango</code></pre>

<img decoding="async" src="https://i.imgur.com/33w2bsR.png" alt="" />  
創建的資料結構如下：  
<img decoding="async" src="https://i.imgur.com/AREpKuM.png" alt="" /> 

執行方式：

<pre class="wp-block-code"><code class="">python manage.py runserver</code></pre>

若想更改默認端口：

<pre class="wp-block-code"><code class="">python manage.py runserver 0.0.0.0:8899</code></pre>

執行成功如下圖：  
<img decoding="async" src="https://i.imgur.com/T83LNyC.png" alt="" /> 

開啟瀏覽器，輸入：

<pre class="wp-block-code"><code class="">http://127.0.0.1:8000/</code></pre>

第一次運行，會看到下圖畫面：  
<img decoding="async" src="https://i.imgur.com/xIuSCBD.png" alt="" /> 

停止方式：Control + C

此時，會多出現一個檔案db.sqlite3  
<img decoding="async" src="https://i.imgur.com/2pFmXot.png" alt="" /> 

Django主要提供了四種數據庫引擎：

<ol class="wp-block-list">
  <li>
    django.db.backends.postgresql
  </li>
  <li>
    django.db.backends.mysql
  </li>
  <li>
    django.db.backends.sqlite3
  </li>
  <li>
    django.db.backends.oracle
  </li>
</ol>

打開setting.py會看到默認引擎是sqlite3，

<pre class="wp-block-code"><code class=""># Database
# https://docs.djangoproject.com/en/3.2/ref/settings/#databases

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/pcR3yH3.png" alt="" /> </figure> 

MySQL設置方式:

<pre class="wp-block-code"><code class="">DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'djangodb',
        'USER': 'root',
        'PASSWORD': '12345',
        'HOST': '127.0.0.1',
    }
}</code></pre>

如果需要更多的配置信息，可以指定配置文件：

<pre class="wp-block-code"><code class="">DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'OPTIONS':{
            'read_default_file': '/path/to/my.cnf',
        },
    }
}</code></pre>

配置文件：

<pre class="wp-block-code"><code class=""># my.cnf
</code></pre>

[client]

databases = djangodb user = root password = 12345 default-character-set=utf8

PostgreSQL數據庫配置:

<pre class="wp-block-code"><code class="">DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'mydatabase',
        'USER': 'mydatabaseuser',
        'PASSWORD': 'mypassword',
        'HOST': '127.0.0.1',
        'PORT': '5432',
    }
}</code></pre>

初始化：

<pre class="wp-block-code"><code class="">python manage.py migrate</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/udBptue.png" alt="" /> </figure> 

### 創建應用程序 

<pre class="wp-block-code"><code class="">python manage.py startapp books</code></pre>

生成books，如下的資料結構

<pre class="wp-block-code"><code class="">.
├── books
│&nbsp;&nbsp; ├── __init__.py
│&nbsp;&nbsp; ├── admin.py
│&nbsp;&nbsp; ├── apps.py
│&nbsp;&nbsp; ├── migrations
│&nbsp;&nbsp; │&nbsp;&nbsp; └── __init__.py
│&nbsp;&nbsp; ├── models.py
│&nbsp;&nbsp; ├── tests.py
│&nbsp;&nbsp; └── views.py
├── db.sqlite3
├── manage.py
└── mydjango
    ├── __init__.py
    ├── asgi.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/RbOLpWV.png" alt="" /> </figure> 

<ul class="wp-block-list">
  <li>
    admin :網站管理設置
  </li>
  <li>
    apps :註冊應用相關
  </li>
  <li>
    migration ：數據庫的升級文件包，會自動升級專案的數據庫
  </li>
  <li>
    models ：定義模型
  </li>
  <li>
    tests :測試相關代碼
  </li>
  <li>
    views ：定義視圖函式
  </li>
</ul>

主要程式撰寫是在views及models

 [1]: https://quietbo.com/2021/06/27/mac-pro-m1-%e5%ae%89%e8%a3%9dvirtualenv/