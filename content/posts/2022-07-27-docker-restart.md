---
title: '[Docker] restart'
author: Bocky
type: post
date: 2022-07-27T07:06:09+00:00
url: /2022/07/27/docker-restart/
categories:
  - 'Docker&amp; Docker-compose'
tags:
  - docker

---
原文檔:

<ul class="wp-block-list">
  <li>
    <a href="https://docs.docker.com/engine/reference/commandline/restart/">Docker Doc</a>
  </li>
  <li>
    <a href="https://docs.docker.com/config/containers/start-containers-automatically/#use-a-restart-policy">Start containers automatically</a>
  </li>
</ul>

只要重開機後, 就要手動去開啟容器, 雖然有GUI很方便按個按鈕就好, 可是有時候還是會忘記要啟動必要容器…

## 設置重啟策略 

<pre class="wp-block-code"><code lang="bash" class="language-bash">docker run --restart={Policy} {Container Name}</code></pre>

此命令更改已在運行的容器:

<pre class="wp-block-code"><code lang="bash" class="language-bash">docker update --restart={Policy} {Container Name}</code></pre>

下方為Policy與原檔描述<figure class="wp-block-table">

| Policy                   | Result                                                                      |
| ------------------------ | --------------------------------------------------------------------------- |
| no                       | 默認, 不要自動重啟容器。                                                               |
| on-failure[:max-retries] | 如果容器因錯誤退出，則重新啟動容器，這表現為非零退出代碼。或者，使用該:max-retries選項限制 Docker 守護程序嘗試重新啟動容器的次數。 |
| always                   | 無論退出狀態如何，始終重新啟動容器。                                                          |
| unless-stopped           | 無論退出狀態如何，始終重啟容器，包括在守護進程啟動時，除非容器在 Docker 守護進程停止之前進入停止狀態。                     |</figure> 

## 查看容器設置 

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ docker inspect {Container Name}</code></pre>

或使用下方指令

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ docker inspect -f "{{ .HostConfig.RestartPolicy }}" {Container_Name}

{always 0}</code></pre>

在HostConfig.RestartPolicy下可以看到已經被改為always  
<img decoding="async" src="https://i.imgur.com/R7L5RQM.png" alt="" /> 

顯示所有正在運行的 docker 容器的重啟策略

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ docker inspect --format "{{.HostConfig.RestartPolicy.Name}}, {{.Name}}, {{.Id}}" $(docker ps -qf status=running) | sort -t, -k1 |column -s, -t</code></pre>

顯示結果:

<pre class="wp-block-code"><code lang="bash" class="language-bash">always   /agitated_hertz   32a0f056b137401990aff0c2532de951933bf301f6736bc806ef5e2490aea2b5
always   /ubuntu           0c1e12f31e1ad359530a2709a3a814e8a442fea756d1cda8694d8c9aebb05755</code></pre>

參考來源:[[stackoverflow]Is it possible to show the restart policy of a running Docker container?][1]

 [1]: https://stackoverflow.com/questions/43108227/is-it-possible-to-show-the-restart-policy-of-a-running-docker-container