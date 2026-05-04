---
title: '[Docker] 建立群組 – Got permission denied while trying to connect to the Docker daemon socket at unix(解決)'
author: Bocky
type: post
date: 2022-06-06T07:43:23+00:00
url: /2022/06/06/docker-建立群組-got-permission-denied-while-trying-to-connect-to-the-docker-daemon-socket-at-unix解決/
categories:
  - Docker
  - Docker-Compose
tags:
  - docker

---
環境:linux

下方錯誤訊息，表示目前的使用者身分沒有權限。

<pre class="wp-block-code"><code lang="bash" class="language-bash">Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/build?buildargs=%7B%7D&cachefrom=%5B%5D&cgroupparent=&cpuperiod=0&cpuquota=0&cpusetcpus=&cpusetmems=&cpushares=0&dockerfile=Dockerfile&labels=%7B%7D&memory=0&memswap=0&networkmode=default&rm=1&shmsize=0&t=ocms_server&target=&ulimits=null&version=1": dial unix /var/run/docker.sock: connect: permission denied</code></pre>

解決方式:

<ol class="wp-block-list">
  <li>
    最前方加入sudo(每次都需要加sudo有點麻煩)
  </li>
  <li>
    將目前使用者加到docker群組裡面(本篇使用的方法)
  </li>
</ol>

# 建立 docker 群組 

<pre class="wp-block-code"><code lang="bash" class="language-bash">sudo groupadd docker</code></pre>

如果一開始就已經有群組的話，就則會告知下方訊息

<pre class="wp-block-code"><code class="">groupadd: group 'docker' already exists</code></pre>

## 將非 root 帳號加上 docker 群組中 

將連接的用戶&#8221;$USER&#8221;添加到docker組。  
如果不想使用當前用戶，請更改用戶名

<pre class="wp-block-code"><code lang="bash" class="language-bash">sudo gpasswd -a $USER docker</code></pre>

成功則返回:

<pre class="wp-block-code"><code class="">Adding user admins to group docker</code></pre>

group 的資訊並不會立刻更新，為了要能立刻產生作用，執行 newgrp docker，

讓這個帳號立刻改成使用 docker 這個群組 (或是你要登出登入也行)：  
執行下方指令, 或注銷/進入以激活對組的更改:

<pre class="wp-block-code"><code class="">newgrp docker</code></pre>

# 重新啟動 docker 服務 

重啟 docker 服務之後，所有的變動就完成了：

<pre class="wp-block-code"><code lang="bash" class="language-bash">sudo systemctl restart docker</code></pre>