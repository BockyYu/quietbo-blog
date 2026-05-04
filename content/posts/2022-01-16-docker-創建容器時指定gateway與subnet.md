---
title: '[Docker] 創建容器時指定gateway與subnet'
author: Bocky
type: post
date: 2022-01-15T18:49:32+00:00
url: /2022/01/16/docker-創建容器時指定gateway與subnet/
categories:
  - Docker
  - Docker-Compose
tags:
  - docker

---
可參考之前的<a href="https://quietbo.com/2022/01/16/docker-%e5%89%b5%e5%bb%ba%e5%92%8c%e4%bd%bf%e7%94%a8-bridge-1/" data-type="URL" data-id="https://quietbo.com/2022/01/16/docker-%e5%89%b5%e5%bb%ba%e5%92%8c%e4%bd%bf%e7%94%a8-bridge-1/">[Docker] 創建和使用 bridge</a>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ docker network create --help

Usage:  docker network create [OPTIONS] NETWORK

Create a network

Options:
      --attachable           Enable manual container attachment
      --aux-address map      Auxiliary IPv4 or IPv6 addresses used by Network driver (default map[])
      --config-from string   The network from which to copy the configuration
      --config-only          Create a configuration only network
  -d, --driver string        Driver to manage the Network (default "bridge")
      --gateway strings      IPv4 or IPv6 Gateway for the master subnet
      --ingress              Create swarm routing-mesh network
      --internal             Restrict external access to the network
      --ip-range strings     Allocate container ip from a sub-range
      --ipam-driver string   IP Address Management Driver (default "default")
      --ipam-opt map         Set IPAM driver specific options (default map[])
      --ipv6                 Enable IPv6 networking
      --label list           Set metadata on a network
  -o, --opt map              Set driver specific options (default map[])
      --scope string         Control the network's scope
      --subnet strings       Subnet in CIDR format that represents a network segment</code></pre>

<pre class="wp-block-code"><code lang="bash" class="language-bash">docker network create -d bridge --gateway 172.200.0.1 --subnet 172.200.0.0/16 demo</code></pre>

查看剛才創建的demo

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ docker network inspect demo
[
    {
        "Name": "demo",
        "Id": "9a5ccdbfa5b5e9968cedb3a9b66b5714e35eade805582538bde47c187e593df5",
        "Created": "2022-01-15T18:42:53.457025805Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.200.0.0/16",
                    "Gateway": "172.200.0.1"
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

建立box4

<pre class="wp-block-code"><code lang="bash" class="language-bash">docker container run -d --rm --name box4 --network demo busybox /bin/sh -c "while true; do sleep 3600; done"</code></pre>

將原本的box3新增demo的網路並ping看看有沒有辦法互通

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">docker network connect demo box3
docker exec -it box4 ping box3</code></pre>

可以使用ip，或是容器名。  
<img decoding="async" src="https://i.imgur.com/6y7gu0v.png" alt="" /> 

或是反過來，用box3來pintbox4也是能相通的。

<pre class="wp-block-code"><code lang="bash" class="language-bash">docker exec -it box3 ping box4</code></pre>