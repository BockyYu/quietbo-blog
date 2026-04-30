---
title: '[Doris] docker容器啟動時遇到 Please set vm.max_map_count to be xxxxxx'
author: Bocky
type: post
date: 2024-10-24T07:51:39+00:00
url: /2024/10/24/doris-docker容器啟動時遇到-please-set-vm-max_map_count-to-be-xxxxxx/
categories:
  - Database
tags:
  - docker
  - doris

---
</p> 

如果在docker 中遇到下方字串</p> 

<pre class="wp-block-code"><code lang="bash" class="language-bash">Please set vm.max_map_count to be 2000000 under root using 'sysctl -w vm.max_map_count=2000000'</code></pre></p> 

使用下方指令</p> 

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">docker run -it --privileged --pid=host --name=change_count debian nsenter -t 1 -m -u -n -i sh</code></pre></p> 

進入到容器後再執行指令：</p> 

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">sysctl -w vm.max_map_count=2000000</code></pre></p> 

\`  
然後exit退出並建立Doris Docker叢集。</p> 

來源來自:[doris官方文件-#Docker部署Doris][1]</p>

 [1]: https://doris.apache.org/docs/1.2/install/construct-docker/run-docker-cluster/#deploy-doris-docker