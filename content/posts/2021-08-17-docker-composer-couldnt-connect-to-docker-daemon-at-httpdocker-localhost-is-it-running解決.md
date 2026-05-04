---
title: '[Docker-Composer] Couldn’t connect to Docker daemon at http+docker://localhost – is it running?(解決)'
author: Bocky
type: post
date: 2021-08-17T07:22:02+00:00
url: /2021/08/17/docker-composer-couldnt-connect-to-docker-daemon-at-httpdocker-localhost-is-it-running解決/
categories:
  - Docker
  - Docker-Compose

---
部屬的環境是用docker-composer，某天用ssh連回去，要下docker指令就出現下面訊息:

<pre class="wp-block-code"><code lang="bash" class="language-bash">ERROR: Couldn't connect to Docker daemon at http+docker://localhost - is it running?

If it's at a non-standard location, specify the URL with the DOCKER_HOST environment variable.
make: *** [Makefile:26: restart] Error 1</code></pre>

這用google翻譯過來看是:

<pre class="wp-block-code"><code class="">無法通過 http+docker://localhost 連接到 Docker 守護進程 - 它是否正在運行？</code></pre>

嗯…….(什麼東西，好不直覺)

<p style="font-size:25px">
  其實就是<strong>忘記加入docker群組</strong>呀!!!
</p>

## 解決方式 

<ol class="wp-block-list">
  <li>
    在機器內下指令，將docker加入群組
  </li>
</ol>

<pre class="wp-block-code"><code lang="docker" class="language-docker">sudo gpasswd -a ${USER} docker</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/mMJyzQ0.png" alt="" /> </figure> 

<ol class="wp-block-list" start="2">
  <li>
    退出當前用戶
  </li>
</ol>

<pre class="wp-block-code"><code lang="docker" class="language-docker">sudo su</code></pre>

<ol class="wp-block-list" start="3">
  <li>
    切換為原本用戶<br />下方ubuntu需依照不同用戶名稱去更改。
  </li>
</ol>

<pre class="wp-block-code"><code lang="docker" class="language-docker">su ubuntu</code></pre>

<ol class="wp-block-list" start="4">
  <li>
    在終端機下docekr指令試試看吧
  </li>
</ol>