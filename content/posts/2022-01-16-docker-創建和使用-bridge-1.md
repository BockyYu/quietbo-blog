---
title: '[Docker] 創建和使用 bridge'
author: Bocky
type: post
date: 2022-01-15T18:38:33+00:00
url: /2022/01/16/docker-創建和使用-bridge-1/
categories:
  - Docker
  - Docker-Compose

---
<div id="ez-toc-container" class="ez-toc-v2_0_82_2 ez-toc-wrap-center counter-hierarchy ez-toc-counter ez-toc-grey ez-toc-container-direction">
  <div class="ez-toc-title-container">
    <p class="ez-toc-title" style="cursor:inherit">
      Table of Contents
    </p>
    
    <span class="ez-toc-title-toggle"><a href="#" class="ez-toc-pull-right ez-toc-btn ez-toc-btn-xs ez-toc-btn-default ez-toc-toggle" aria-label="顯示/隱藏內容目錄"><span class="ez-toc-js-icon-con"><span class=""><span class="eztoc-hide" style="display:none;">Toggle</span><span class="ez-toc-icon-toggle-span"><svg style="fill: #999;color:#999" xmlns="http://www.w3.org/2000/svg" class="list-377408" width="20px" height="20px" viewBox="0 0 24 24" fill="none"><path d="M6 6H4v2h2V6zm14 0H8v2h12V6zM4 11h2v2H4v-2zm16 0H8v2h12v-2zM4 16h2v2H4v-2zm16 0H8v2h12v-2z" fill="currentColor"></path></svg><svg style="fill: #999;color:#999" class="arrow-unsorted-368013" xmlns="http://www.w3.org/2000/svg" width="10px" height="10px" viewBox="0 0 24 24" version="1.2" baseProfile="tiny"><path d="M18.2 9.3l-6.2-6.3-6.2 6.3c-.2.2-.3.4-.3.7s.1.5.3.7c.2.2.4.3.7.3h11c.3 0 .5-.1.7-.3.2-.2.3-.5.3-.7s-.1-.5-.3-.7zM5.8 14.7l6.2 6.3 6.2-6.3c.2-.2.3-.5.3-.7s-.1-.5-.3-.7c-.2-.2-.4-.3-.7-.3h-11c-.3 0-.5.1-.7.3-.2.2-.3.5-.3.7s.1.5.3.7z"/></svg></span></span></span></a></span>
  </div><nav>
  
  <ul class='ez-toc-list ez-toc-list-level-1 ' >
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2022/01/16/docker-%e5%89%b5%e5%bb%ba%e5%92%8c%e4%bd%bf%e7%94%a8-bridge-1/#%E5%BB%BA%E7%AB%8B%E4%B8%80%E5%80%8B%E8%87%AA%E8%A8%82%E5%90%8D%E7%A8%B1%E7%9A%84_docker_network" >建立一個自訂名稱的 docker network</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2022/01/16/docker-%e5%89%b5%e5%bb%ba%e5%92%8c%e4%bd%bf%e7%94%a8-bridge-1/#%E5%89%B5%E5%BB%BA%E4%B8%80%E5%80%8B%E5%AE%B9%E5%99%A8" >創建一個容器</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2022/01/16/docker-%e5%89%b5%e5%bb%ba%e5%92%8c%e4%bd%bf%e7%94%a8-bridge-1/#%E8%AE%93%E4%B8%80%E5%80%8B%E5%AE%B9%E5%99%A8%E9%80%A3%E6%8E%A52%E5%80%8B%E7%B6%B2%E8%B7%AF" >讓一個容器連接2個網路</a>
    </li>
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2022/01/16/docker-%e5%89%b5%e5%bb%ba%e5%92%8c%e4%bd%bf%e7%94%a8-bridge-1/#%E6%96%B7%E9%96%8B%E5%AE%B9%E5%99%A8%E8%88%87%E7%B6%B2%E7%B5%A1%E7%9A%84%E9%80%A3%E6%8E%A5" >斷開容器與網絡的連接</a>
    </li>
  </ul></nav>
</div>

## <span class="ez-toc-section" id="%E5%BB%BA%E7%AB%8B%E4%B8%80%E5%80%8B%E8%87%AA%E8%A8%82%E5%90%8D%E7%A8%B1%E7%9A%84_docker_network"></span>建立一個自訂名稱的 docker network<span class="ez-toc-section-end"></span> 

建立一個自訂名稱的 docker network，這邊取名為mybridge:

<pre class="wp-block-code"><code lang="bash" class="language-bash">docker network create -d bridge mybridge</code></pre>

查看目前network的訊息，是否有我們建立的mybridge

<pre class="wp-block-code"><code lang="bash" class="language-bash">docker network ls</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/nnT1EXU.png" alt="" /> </figure> 

查看mybridge的資訊。

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ docker network inspect mybridge
[
    {
        "Name": "mybridge",
        "Id": "8569e3bba27a4dd6a5f1a8d39c9df7350aa27dc8eb38118ab4b99f9fb4b6e7cf",
        "Created": "2022-01-15T14:21:30.014726296Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {},
        "Options": {},
        "Labels": {}
    }
]</code></pre>

## <span class="ez-toc-section" id="%E5%89%B5%E5%BB%BA%E4%B8%80%E5%80%8B%E5%AE%B9%E5%99%A8"></span>創建一個容器<span class="ez-toc-section-end"></span> 

將容器指定network在mybridge

<ul class="wp-block-list">
  <li>
    &#8211;network :後方帶入網路名
  </li>
</ul>

<pre class="wp-block-code"><code lang="bash" class="language-bash">docker container run -d --rm --name box3 --network mybridge busybox /bin/sh -c "while true; do sleep 3600; done"</code></pre>

查看box3的訊息，最下方Networks:

<pre class="wp-block-code"><code lang="basic" class="language-basic">"Networks": {
                "mybridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": [
                        "7ad11d3a4e9c"
                    ],
                    "NetworkID": "8569e3bba27a4dd6a5f1a8d39c9df7350aa27dc8eb38118ab4b99f9fb4b6e7cf",
                    "EndpointID": "213898adbc0abf4dc37894e94f10720f44682b59d046a45f9a88ed92172bf306",
                    "Gateway": "172.18.0.1",
                    "IPAddress": "172.18.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:12:00:02",
                    "DriverOpts": null
                }
            }</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/bxWulUI.png" alt="" /> </figure> 

回來查看mybridge，會發現有一個新的容器(box3)資料

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ docker network inspect mybridge
[
    {
        "Name": "mybridge",
        "Id": "8569e3bba27a4dd6a5f1a8d39c9df7350aa27dc8eb38118ab4b99f9fb4b6e7cf",
        "Created": "2022-01-15T14:21:30.014726296Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "7ad11d3a4e9c0fff207c329a9beae2fc8060b0110a67dc4a32f133c591be4abb": {
                "Name": "box3",
                "EndpointID": "213898adbc0abf4dc37894e94f10720f44682b59d046a45f9a88ed92172bf306",
                "MacAddress": "02:42:ac:12:00:02",
                "IPv4Address": "172.18.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]</code></pre>

## <span class="ez-toc-section" id="%E8%AE%93%E4%B8%80%E5%80%8B%E5%AE%B9%E5%99%A8%E9%80%A3%E6%8E%A52%E5%80%8B%E7%B6%B2%E8%B7%AF"></span>讓一個容器連接2個網路<span class="ez-toc-section-end"></span> 

原本的box1與box2是連接預設的docker0(就是bridge)，而box3是連接mybridge

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ docker network ls
NETWORK ID     NAME       DRIVER    SCOPE
b2077f8151cb   bridge     bridge    local
d1465da885e1   host       host      local
8569e3bba27a   mybridge   bridge    local
91fc3c2b25fb   none       null      local</code></pre>

讓box3連接bridge網路，再查看一次box3的網路資訊:

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">docker network connect bridge box3
docker inspect box3</code></pre>

原本box3只有一個mybridge，新增連接後的Networks出現了bridge的資料。

<pre class="wp-block-code"><code lang="bash" class="language-bash">"Networks": {
                "bridge": {
                    "IPAMConfig": {},
                    "Links": null,
                    "Aliases": [],
                    "NetworkID": "b2077f8151cbe85b063e14c0603ad241acc0066d0155b747d09d5a1171598b62",
                    "EndpointID": "d7ee13480da9ec15d24ced9a42acc24da4344577bf4832b2e927791c4e8d9155",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.6",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:06",
                    "DriverOpts": {}
                },
                "mybridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": [
                        "7ad11d3a4e9c"
                    ],
                    "NetworkID": "8569e3bba27a4dd6a5f1a8d39c9df7350aa27dc8eb38118ab4b99f9fb4b6e7cf",
                    "EndpointID": "213898adbc0abf4dc37894e94f10720f44682b59d046a45f9a88ed92172bf306",
                    "Gateway": "172.18.0.1",
                    "IPAddress": "172.18.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:12:00:02",
                    "DriverOpts": null
                }
            }</code></pre>

進入到box3來查看ip a的狀態，  
eth0屬於mybridge，eth1屬於bridge。  
<img decoding="async" src="https://i.imgur.com/XGrrGgI.png" alt="" /> 

## <span class="ez-toc-section" id="%E6%96%B7%E9%96%8B%E5%AE%B9%E5%99%A8%E8%88%87%E7%B6%B2%E7%B5%A1%E7%9A%84%E9%80%A3%E6%8E%A5"></span>斷開容器與網絡的連接<span class="ez-toc-section-end"></span> 

查看網路相關命令：

<pre class="wp-block-code"><code lang="bash" class="language-bash">docker network</code></pre>

<pre class="wp-block-code"><code lang="bash" class="language-bash">Usage:  docker network COMMAND

Manage networks

Commands:
  connect     Connect a container to a network
  create      Create a network
  disconnect  Disconnect a container from a network
  inspect     Display detailed information on one or more networks
  ls          List networks
  prune       Remove all unused networks
  rm          Remove one or more networks

Run 'docker network COMMAND --help' for more information on a command.</code></pre>

斷開box3與bridge網絡的連接，並查詢box3

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">docker network disconnect bridge box3
docker inspect box3</code></pre>

結果如下，Networks只剩下mybridge:

<pre class="wp-block-code"><code lang="bash" class="language-bash">"Networks": {
                "mybridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": [
                        "7ad11d3a4e9c"
                    ],
                    "NetworkID": "8569e3bba27a4dd6a5f1a8d39c9df7350aa27dc8eb38118ab4b99f9fb4b6e7cf",
                    "EndpointID": "213898adbc0abf4dc37894e94f10720f44682b59d046a45f9a88ed92172bf306",
                    "Gateway": "172.18.0.1",
                    "IPAddress": "172.18.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:12:00:02",
                    "DriverOpts": null
                }
            }</code></pre>

網路圖如下:  
<img decoding="async" src="https://i.imgur.com/zzA6Mbr.png" alt="" />