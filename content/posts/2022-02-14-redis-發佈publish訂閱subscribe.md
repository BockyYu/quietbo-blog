---
title: '[Redis] 發佈(publish)&訂閱(subscribe)'
author: Bocky
type: post
date: 2022-02-14T10:51:45+00:00
url: /2022/02/14/redis-發佈publish訂閱subscribe/
categories:
  - Redis
tags:
  - redis

---
環境:Windows 10  
Redis: 5.0.7

Redis發布訂閱(pub/sub) 是一種消息通信模式：發送者(pub) 發送消息，訂閱者(sub) 接收消息。

## 範例 {#範例.wp-block-heading}

創建了訂閱頻道名為runoobChat  
訂閱之後就無法在進行操作，只能點擊Stop Subscribe  
<img decoding="async" src="https://i.imgur.com/pGIes6o.png" alt="" /> 

開新的GUI連到redis內，查看訂閱數:

<pre class="wp-block-code"><code class="">pubsub numsub channel_name </code></pre>

返回頻道訂閱者的數量:  
<img decoding="async" src="https://i.imgur.com/5ibVYq8.png" alt="" /> 

channels可創建多個，且可同時被多個client訂閱，client可訂閱多個channels(如下圖)<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/hSH0f5U.png" alt="" /> </figure> 

<pre class="wp-block-code"><code lang="jsx" class="language-jsx">subscribe channel_name # 訂閱1個channel
subscribe channel_name_1 channel_name_2 # 訂閱多個channel</code></pre>

將信息發送到指定的頻道，下方是runoobChat發送訊息出去給所有訂閱者。

<pre class="wp-block-code"><code class="">publish runoobChat "發送的訊息" </code></pre>

下圖是我開啟3個redis，前面2個是client，最右方的是server，發送訊息給訂閱runoobChat這個channel的client。<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/SjxSEMt.png" alt="" /> </figure> 

[Redis文檔][1]  
[Redis 發布訂閱][2]

 [1]: https://redis.io/topics/pubsub
 [2]: https://www.runoob.com/redis/redis-pub-sub.html