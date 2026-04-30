---
title: '[Ubuntu] Ubuntu22網卡遺失'
author: Bocky
type: post
date: 2023-01-10T04:47:46+00:00
url: /2023/01/10/ubuntu-ubuntu22網卡遺失/
categories:
  - 系統相關

---
某天工作發現右上角網路的標誌整個不見…

<ol class="wp-block-list">
  <li>
    先確認網卡是否正常
  </li>
</ol>

<pre class="wp-block-code"><code class="">$sudo lshw -c network</code></pre>

若有出現logical name: ens33代表正常  
<img decoding="async" src="https://i.imgur.com/DkZQcZl.png" alt="" /> 

<ol class="wp-block-list" start="2">
  <li>
    執行下方指令
  </li>
</ol>

<pre class="wp-block-code"><code class="">sudo service NetworkManager stop
sudo rm  /var/lib/NetworkManager/NetworkManager.state
sudo gedit /etc/NetworkManager/NetworkManager.conf </code></pre>

把managed=false改為managed=true再儲存。  
<img decoding="async" src="https://i.imgur.com/SKDCFmk.png" alt="" /> 

執行下方指令後，右上角就會出現網路

<pre class="wp-block-code"><code class="">sudo service NetworkManager start</code></pre>

完成  
<img decoding="async" src="https://i.imgur.com/Q52Rcli.png" alt="" />