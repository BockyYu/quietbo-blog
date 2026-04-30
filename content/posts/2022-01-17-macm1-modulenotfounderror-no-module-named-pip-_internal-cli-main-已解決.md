---
title: '[Mac|M1] ModuleNotFoundError: No module named ‘pip._internal.cli.main’ (已解決)'
author: Bocky
type: post
date: 2022-01-17T07:01:50+00:00
url: /2022/01/17/macm1-modulenotfounderror-no-module-named-pip-_internal-cli-main-已解決/
categories:
  - Python
  - 系統相關
tags:
  - mac

---
問題訊息如下:

<pre class="wp-block-code"><code class="">$ pip install --upgrade pip
Traceback (most recent call last):
  File "/usr/local/bin/pip", line 6, in &lt;module&gt;
    from pip._internal.cli.main import main
ModuleNotFoundError: No module named 'pip._internal.cli.main'</code></pre>

解決方式:

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3 get-pip.py --force-reinstall</code></pre>

<pre class="wp-block-code"><code class="">Defaulting to user installation because normal site-packages is not writeable
Collecting pip
  Using cached pip-21.3.1-py3-none-any.whl (1.7 MB)
Installing collected packages: pip
  WARNING: The scripts pip, pip3 and pip3.8 are installed in '/Users/bocky/Library/Python/3.8/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
Successfully installed pip-21.3.1
WARNING: You are using pip version 19.2.3; however, version 21.3.1 is available.
You should consider upgrading via the '/Applications/Xcode.app/Contents/Developer/usr/bin/python3 -m pip install --upgrade pip' command.</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/ZxKs6aB.png" alt="" /> </figure> 

訊息告知建議執行的內容:

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">/Applications/Xcode.app/Contents/Developer/usr/bin/python3 -m pip install --upgrade pip</code></pre>

下方為執行結果:

<pre class="wp-block-code"><code class="">Defaulting to user installation because normal site-packages is not writeable
Requirement already satisfied: pip in ./Library/Python/3.8/lib/python/site-packages (21.3.1)</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/LwzulX6.png" alt="" /> </figure> 

解決!