---
title: '[安裝]Python 2.7以及Python virtualenv'
author: Bocky
type: post
date: 2021-03-24T10:51:20+00:00
url: /2021/03/24/python-2-7以及python-virtual-environment-安裝/
categories:
  - Python
tags:
  - 安裝

---
因ubuntu從18.04開始，內建的python版本都是為3.6以上 (舊的內建2.7)，所以要手動輸入版本號

<div id="ez-toc-container" class="ez-toc-v2_0_82_2 ez-toc-wrap-center counter-hierarchy ez-toc-counter ez-toc-grey ez-toc-container-direction">
  <div class="ez-toc-title-container">
    <p class="ez-toc-title" style="cursor:inherit">
      Table of Contents
    </p>
    
    <span class="ez-toc-title-toggle"><a href="#" class="ez-toc-pull-right ez-toc-btn ez-toc-btn-xs ez-toc-btn-default ez-toc-toggle" aria-label="顯示/隱藏內容目錄"><span class="ez-toc-js-icon-con"><span class=""><span class="eztoc-hide" style="display:none;">Toggle</span><span class="ez-toc-icon-toggle-span"><svg style="fill: #999;color:#999" xmlns="http://www.w3.org/2000/svg" class="list-377408" width="20px" height="20px" viewBox="0 0 24 24" fill="none"><path d="M6 6H4v2h2V6zm14 0H8v2h12V6zM4 11h2v2H4v-2zm16 0H8v2h12v-2zM4 16h2v2H4v-2zm16 0H8v2h12v-2z" fill="currentColor"></path></svg><svg style="fill: #999;color:#999" class="arrow-unsorted-368013" xmlns="http://www.w3.org/2000/svg" width="10px" height="10px" viewBox="0 0 24 24" version="1.2" baseProfile="tiny"><path d="M18.2 9.3l-6.2-6.3-6.2 6.3c-.2.2-.3.4-.3.7s.1.5.3.7c.2.2.4.3.7.3h11c.3 0 .5-.1.7-.3.2-.2.3-.5.3-.7s-.1-.5-.3-.7zM5.8 14.7l6.2 6.3 6.2-6.3c.2-.2.3-.5.3-.7s-.1-.5-.3-.7c-.2-.2-.4-.3-.7-.3h-11c-.3 0-.5.1-.7.3-.2.2-.3.5-.3.7s.1.5.3.7z"/></svg></span></span></span></a></span>
  </div><nav>
  
  <ul class='ez-toc-list ez-toc-list-level-1 ' >
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2021/03/24/python-2-7%e4%bb%a5%e5%8f%8apython-virtual-environment-%e5%ae%89%e8%a3%9d/#%E5%AE%89%E8%A3%9Dpython27" >安裝python2.7</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2021/03/24/python-2-7%e4%bb%a5%e5%8f%8apython-virtual-environment-%e5%ae%89%e8%a3%9d/#%E5%AE%89%E8%A3%9Dpip%E5%A5%97%E4%BB%B6" >安裝pip套件</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2021/03/24/python-2-7%e4%bb%a5%e5%8f%8apython-virtual-environment-%e5%ae%89%e8%a3%9d/#%E4%BD%BF%E7%94%A8pip%E5%AE%89%E8%A3%9Dvirtualenv" >使用pip安裝virtualenv</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2021/03/24/python-2-7%e4%bb%a5%e5%8f%8apython-virtual-environment-%e5%ae%89%e8%a3%9d/#%E7%82%BAvirtualenv%E8%A3%BD%E4%BD%9C%E5%88%A5%E5%90%8D" >為virtualenv製作別名</a>
    </li>
  </ul></nav>
</div>

## <span class="ez-toc-section" id="%E5%AE%89%E8%A3%9Dpython27"></span>安裝python2.7<span class="ez-toc-section-end"></span> {.wp-block-heading}

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">sudo apt update
sudo apt install python2.7 -y</code></pre>

檢查一下python2.7版本:

<pre class="wp-block-code"><code lang="bash" class="language-bash">python2.7 -V</code></pre>

輸出結果:  
<img decoding="async" src="https://i.imgur.com/w4o7c6Q.png" alt="" /> 

## <span class="ez-toc-section" id="%E5%AE%89%E8%A3%9Dpip%E5%A5%97%E4%BB%B6"></span>安裝pip套件<span class="ez-toc-section-end"></span> {.wp-block-heading}

這邊的作法是下載`get-pip.py`來安裝。

**注意**:  
第3行的URL不一定是最新的，若有跳出錯誤訊息是URL找不到，請自行更換成錯誤訊息跳出的URL。

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">cd ~
cd 下載
curl https://bootstrap.pypa.io/pip/2.7/get-pip.py -o get-pip.py
python2.7 get-pip.py </code></pre>

若安裝成功，最後會看到這個訊息:  
<img decoding="async" src="https://i.imgur.com/UIkuliG.png" alt="" /> 

(可略過不做)  
為使用pip套件建立別名:  
後面的指令pip2請自行改成`python2.7 -m pip`

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">cd ~
touch .bash_aliases
echo "alias pip2='python2.7 -m pip'" &gt;&gt; .bash_aliases
source .bash_aliases
pip2 -V</code></pre>

輸出結果:

<pre class="wp-block-code"><code lang="bash" class="language-bash">pip 20.3.4 from /home/ubuntu/.local/lib/python2.7/site-packages/pip (python 2.7)</code></pre>

## <span class="ez-toc-section" id="%E4%BD%BF%E7%94%A8pip%E5%AE%89%E8%A3%9Dvirtualenv"></span>使用pip安裝virtualenv<span class="ez-toc-section-end"></span> {.wp-block-heading}

日後為每個專案製作一個專屬的python environment

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">pip2 install virtualenv
# 等同於 python2.7 -m pip install virtualenv</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/u9rTOFG.png" alt="" /> </figure> 

## <span class="ez-toc-section" id="%E7%82%BAvirtualenv%E8%A3%BD%E4%BD%9C%E5%88%A5%E5%90%8D"></span>為virtualenv製作別名<span class="ez-toc-section-end"></span> {.wp-block-heading}

這是因為如果安裝其他python版本的virtualenv，用別名來區分使用的版本。**也可以略過，後續指令virtialenv2.7自行替換成virtualenv**

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">echo "alias virtualenv2.7='python2.7 -m virtualenv'" &gt;&gt; ~/.bash_aliases
source .bash_aliases
# 測試一下
virtualenv2.7 --version
# 輸出結果
# virtualenv 20.4.3 from /home/ubuntu/.local/lib/python2.7/site-packages/virtualenv/__init__.pyc</code></pre>

製作一個test_venv專屬的python environment。

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">mkdir python27_venv
cd python27_venv
virtualenv2.7 test_venv  # 方法1:有製作別名(上方操作)才可使用此方法
python27_venv python2.7 -m virtualenv test_venv  # 方法2</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/IBxbyKT.png" alt="" /> </figure> 

創建完後進入虛擬環境:

<pre class="wp-block-code"><code lang="bash" class="language-bash">source ~/python27_venv/test_venv/bin/activate</code></pre>

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers"># 命令列多出前綴(test_venv)。表示已經啟用此虛擬環境
(test_venv)$ python -V
Python 2.7.17 # 輸出結果
(test_venv)$ pip list

(test_venv)$ deactivate # 離開虛擬環境

# 前綴消失，表示已經關閉虛擬環境</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/YhCSlD5.png" alt="" /> </figure> <figure class="wp-block-image"><img decoding="async" src="https://i.imgur.com/xuP235Q.png" alt="" /></figure>