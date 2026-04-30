---
title: '[Docker] Docker Bridge 網路'
author: Bocky
type: post
date: 2022-01-14T15:14:13+00:00
url: /2022/01/14/docker-docker-bridge-網路/
categories:
  - 'Docker&amp; Docker-compose'
tags:
  - docker

---
## 容器間通信 {.wp-block-heading}

容器都連接到了一個叫 docker0 的Linux bridge上

<pre class="wp-block-code"><code class="">$ docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
b2077f8151cb   bridge    bridge    local
d1465da885e1   host      host      local
91fc3c2b25fb   none      null      local</code></pre>

下方為bridge的訊息，基本上Containers的IPv4Address會在Subnet的子網內。

<pre class="wp-block-code"><code class="">$ docker network inspect b20
[
    {
        "Name": "bridge",
        "Id": "b2077f8151cbe85b063e14c0603ad241acc0066d0155b747d09d5a1171598b62",
        "Created": "2022-01-05T06:05:45.888144625Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.17.0.0/16",
                    "Gateway": "172.17.0.1"
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
            "0f74d05e5298f06e21b056273867145558143b4dda2b62f0e397ef31f25fc074": {
                "Name": "box1",
                "EndpointID": "8b7adf5422e5701c9fd762728009809a5a63033cdfe1ea2d621fb3d6a668f4ec",
                "MacAddress": "02:42:ac:11:00:02",
                "IPv4Address": "172.17.0.2/16",
                "IPv6Address": ""
            },
            "5360d3a4fb4ab3fab6b4b3fc505932f9360bc5d970d1411db8acd84be37d0338": {
                "Name": "web2",
                "EndpointID": "b318ba87a14cc6bb72183805479d0acc35947045242875b2bd590290bdde03ca",
                "MacAddress": "02:42:ac:11:00:03",
                "IPv4Address": "172.17.0.3/16",
                "IPv6Address": ""
            },
            "d9875a0e49cd74897dc3d25d7d9ad297bcfbd62bdfde050ddb2e64b5cf5764e0": {
                "Name": "box2",
                "EndpointID": "67c774ac6dbac5d7266223d34ff28a0a81c2f24074397ce307d8e49593e5f950",
                "MacAddress": "02:42:ac:11:00:05",
                "IPv4Address": "172.17.0.5/16",
                "IPv6Address": ""
            },
            "f8b413a00b3b4715914b381a28b1aef8816dc32942d6ec2eb29c2570da3069ff": {
                "Name": "web1",
                "EndpointID": "96c5cbd408523c17fae501ce51c2cb1b6d85ab4d70d629b88e630f7faabc336d",
                "MacAddress": "02:42:ac:11:00:04",
                "IPv4Address": "172.17.0.4/16",
                "IPv6Address": ""
            }
        },
        "Options": {
            "com.docker.network.bridge.default_bridge": "true",
            "com.docker.network.bridge.enable_icc": "true",
            "com.docker.network.bridge.enable_ip_masquerade": "true",
            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
            "com.docker.network.bridge.name": "docker0",
            "com.docker.network.driver.mtu": "1500"
        },
        "Labels": {}
    }
]</code></pre>



並且Containers都默認的連接到docker0，如下圖。<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/mqnWun0.png" alt="" /> </figure> <figure class="wp-block-image size-large"><img loading="lazy" decoding="async" width="1024" height="668" src="https://quietbo.com/wp-content/uploads/2022/01/image-1024x668.png" alt="" class="wp-image-693" srcset="https://quietbo.com/wp-content/uploads/2022/01/image-1024x668.png 1024w, https://quietbo.com/wp-content/uploads/2022/01/image-300x196.png 300w, https://quietbo.com/wp-content/uploads/2022/01/image-768x501.png 768w, https://quietbo.com/wp-content/uploads/2022/01/image.png 1316w" sizes="auto, (max-width: 1024px) 100vw, 1024px" /></figure>