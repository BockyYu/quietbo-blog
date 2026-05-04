---
title: '[Mac] 安裝Jenkins，並與github連接'
author: Bocky
type: post
date: 2021-12-11T18:24:19+00:00
url: /2021/12/12/mac-安裝jenkins並與github連接/
categories:
  - Git
  - Jenkins
tags:
  - GIT
  - jenkins
  - m1

---
使用Mac M1  
Jenkins 2.319.1

# 安裝Jenkins 

到[Jenkins網站][1]下載對應的檔案。目前我是使用

<pre class="wp-block-code"><code lang="bash" class="language-bash">brew install jenkins-lts</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/OzpWOTs.png" alt="" /> </figure> 

安裝完成後，啟動jenkins

<pre class="wp-block-code"><code lang="bash" class="language-bash">brew services start jenkins-lts</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/sZkyWrq.png" alt="" /> </figure> 

打開瀏覽器，輸入：

<pre class="wp-block-code"><code class="">http://localhost:8080</code></pre>

一進去jenkins會要求使用密碼解鎖，初始密碼的路徑，就在提示上的紅色字。  
<img decoding="async" src="https://i.imgur.com/mJtjOa2.png" alt="" /> 

解鎖後，選擇要安裝的套件  
<img decoding="async" src="https://i.imgur.com/pUcbYIe.png" alt="" /> 

接下來是安裝時間，會稍微久一點。  
<img decoding="async" src="https://i.imgur.com/1BcCNOz.png" alt="" /> 

安裝完成後，會要求輸入建立admin帳號，這些帳密都要記住，未來登入需要使用。<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/Wt8Xb8a.png" alt="" /> </figure> <figure class="wp-block-image"><img decoding="async" src="https://i.imgur.com/N3T0Fpj.png" alt="" /></figure> 

成功進入jenkins！  
<img decoding="async" src="https://i.imgur.com/UAg0ro4.png" alt="" /> <figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/Vgj5t8W.png" alt="" /> </figure> 

# 設定 jenkins 與Github Rerository連接 

<ol class="wp-block-list">
  <li>
    新增建置作業<br /><img decoding="async" src="https://i.imgur.com/nwfYR6x.png" alt="" />
  </li>
  <li>
    新增項目名稱，建置Free-Strle軟體專案<br /><img decoding="async" src="https://i.imgur.com/fuImLsu.png" alt="" />
  </li>
  <li>
    輸入github的git網址<br /><img decoding="async" src="https://i.imgur.com/DBTTCi9.png" alt="" />
  </li>
  <li>
    建置觸發程序，將GitHub hook trigger for GITScm polling打勾。<br /><img decoding="async" src="https://i.imgur.com/upQad1U.png" alt="" />
  </li>
  <li>
    建置環境選擇執行Shell，並輸入下方指令後儲存。
  </li>
</ol>

<pre class="wp-block-code"><code lang="bash" class="language-bash">echo 開始建置mydjango</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/4hzqyUk.png" alt="" /> </figure> <figure class="wp-block-image"><img decoding="async" src="https://i.imgur.com/9ucJHQm.png" alt="" /></figure> 

注意：這次示範使用mac的shell，如果使用windows的Shell語法要注意更換。

<ol class="wp-block-list" start="6">
  <li>
    儲存後點擊「馬上建置」，成功後左下方會出現綠色勾，若失敗的話可進入觀看失敗訊息。<br /><img decoding="async" src="https://i.imgur.com/7xd5MZx.png" alt="" />
  </li>
</ol>

建置完成後，點擊「#1」並進入「console output」，就可以看到終端機的輸出了。<figure class="wp-block-image size-full">

<img loading="lazy" decoding="async" width="666" height="806" src="/uploads/2021/12/image.png" alt="" class="wp-image-644" srcset="/uploads/2021/12/image.png 666w, /uploads/2021/12/image-248x300.png 248w" sizes="auto, (max-width: 666px) 100vw, 666px" /> </figure> 

## Jenkins檢查github 

不建議使用，基本上應該是github上有push新的程式後，jenkins再進行建置。  
<img decoding="async" src="https://i.imgur.com/mhftEQP.png" alt="" />

 [1]: https://www.jenkins.io/