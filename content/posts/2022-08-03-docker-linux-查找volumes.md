---
title: '[Docker] Linux 查找volumes'
author: Bocky
type: post
date: 2022-08-03T10:27:42+00:00
url: /2022/08/03/docker-linux-查找volumes/
categories:
  - 'Docker&amp; Docker-compose'
  - Linux
tags:
  - docker
  - linux

---
以下為linux在查找volumes範例

查看已建立的volume

<pre class="wp-block-code"><code class="">$ docker volume list
DRIVER    VOLUME NAME
local     mysql-data</code></pre>

查看該volume資訊, 會看到Mountpoint, 這是存放的路徑

<pre class="wp-block-code"><code class="">$ docker inspect mysql-data
[
    {
        "CreatedAt": "2022-08-03T05:59:51Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/mysql-data/_data",
        "Name": "mysql-data",
        "Options": null,
        "Scope": "local"
    }
]</code></pre>

會發現使用找不到, 因為該路徑下需要使用root

<pre class="wp-block-code"><code class="">$ cd /var/lib/docker/volumes/mysql-data/_data</code></pre>

<pre class="wp-block-code"><code class="">$ sudo -s
$ cd /var/lib/docker/volumes/mysql-data/_data</code></pre>

該路徑下會看到database, 內容會有tableName.ibd