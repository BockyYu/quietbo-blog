---
title: '[Docker] Mac M1 安裝 Docker'
author: Bocky
type: post
date: 2021-09-13T13:07:20+00:00
url: /2021/09/13/docker-安裝-mac-m1/
categories:
  - 'Docker&amp; Docker-compose'
tags:
  - docker
  - 安裝

---
[docker M1晶片安裝網址][1]  
[docker Intel安裝網址][2]  
以往在Linux（ubuntu)環境安裝Docker，都是通過命令行安裝的，但這次 安裝Mac版的Docker變方便許多，下載完成的文件名叫做Docker.dmg。  
雙擊後安裝，完成會出現下圖，把Docker.app移至應用程式就完成了。  
<img decoding="async" src="https://i.imgur.com/Yxy1rgU.png" alt="" /> 

應用程式中找到 Docker，雙擊打開，在右上角就會顯示docker已啟用。  
<img decoding="async" src="https://i.imgur.com/We4WkdA.png" alt="" /> 

系統要求:  
必須安裝Rosetta 2，因為某些二進製文件仍然是 Darwin/AMD64。要從命令行手動安裝 Rosetta 2，請運行以下命令：

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">softwareupdate --install-rosetta</code></pre>

檢查當前docker的版本：

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">docker version</code></pre>

使用M1晶片的話，Arch會是arm64  
<img decoding="async" src="https://i.imgur.com/QaW3kjD.png" alt="" /> 

docker.app打開後的畫面如下：  
<img decoding="async" src="https://i.imgur.com/R5PL8bA.png" alt="" />

 [1]: https://docs.docker.com/docker-for-mac/apple-silicon/
 [2]: https://docs.docker.com/docker-for-mac/install/