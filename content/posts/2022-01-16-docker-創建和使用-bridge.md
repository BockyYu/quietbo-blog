---
title: '[Docker] 創建和使用 bridge'
author: Bocky
type: post
date: 2022-01-15T18:23:58+00:00
url: /2022/01/16/docker-創建和使用-bridge/
categories:
  - Docker
  - Docker-Compose
tags:
  - docker

---
建立一個自訂名稱的 docker network，這邊取名為mybridge:

<pre class="wp-block-code"><code class="">docker network create -d bridge mybridge</code></pre>

查看目前network的訊息，是否有我們建立的mybridge

<pre class="wp-block-code"><code class="">docker network ls</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/nnT1EXU.png" alt="" /> </figure> 

查看mybridge的資訊。

<pre class="wp-block-code"><code class="">$ docker network inspect mybridge
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

創建一個容器，指定network在mybridge

<pre class="wp-block-code"><code class="">docker container run -d --rm --name box3 --network mybridge busybox /bin/sh -c "while true; do sleep 3600; done"</code></pre>

查看box3的訊息，最下方Networks:

<pre class="wp-block-code"><code class="">"Networks": {
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

<pre class="wp-block-code"><code class="">$ docker network inspect mybridge
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

## 讓一個容器連接2個網路 

原本的box1與box2是連接預設的docker0(就是bridge)，而box3是連接mybridge

<pre class="wp-block-code"><code class="">$ docker network ls
NETWORK ID     NAME       DRIVER    SCOPE
b2077f8151cb   bridge     bridge    local
d1465da885e1   host       host      local
8569e3bba27a   mybridge   bridge    local
91fc3c2b25fb   none       null      local</code></pre>

讓box3連接bridge網路，再查看一次box3的網路資訊:

<pre class="wp-block-code"><code class="">docker network connect bridge box3
docker inspect box3</code></pre>

原本box3只有一個mybridge，新增連接後的Networks出現了bridge的資料。

<pre class="wp-block-code"><code class="">"Networks": {
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

## 斷開容器與網絡的連接 

查看網路相關命令：

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">docker network</code></pre>

<pre class="wp-block-code"><code class="">Usage:  docker network COMMAND

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

<pre class="wp-block-code"><code class="">"Networks": {
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