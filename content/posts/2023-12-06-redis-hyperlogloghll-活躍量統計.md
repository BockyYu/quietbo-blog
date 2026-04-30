---
title: '[Redis] HyperLogLog(HLL) – 活躍量統計'
author: Bocky
type: post
date: 2023-12-06T11:00:45+00:00
url: /2023/12/06/redis-hyperlogloghll-活躍量統計/
categories:
  - Redis

---
統計一個APP的日活量（DAU）和月活量（MAU）

<pre class="wp-block-code"><code class="">基數: 不重複元素, 例如{1, 2, 3, 5, 5, 5, 6}, 基數集為{1, 2, 3, 5, 6}, 基數為5;</code></pre>

本次範例使用Docker內建立一個Redis容器  
[Redis-hyperloglogs][1]

HyperLogLogs 提供了3個指令：

<ul class="wp-block-list">
  <li>
    pfadd : 添加
  </li>
  <li>
    pfcount : 計數
  </li>
  <li>
    pfmerge : 合併
  </li>
</ul>

<pre class="wp-block-code"><code class="">&gt; PFADD bikes Hyperion Deimos Phoebe Quaoar
(integer) 1
&gt; PFCOUNT bikes
(integer) 4
&gt; PFADD commuter_bikes Salacia Mimas Quaoar
(integer) 1
&gt; PFMERGE all_bikes bikes commuter_bikes
OK
&gt; PFCOUNT all_bikes
(integer) 6</code></pre>

以上的操作說明為:

<ol class="wp-block-list">
  <li>
    將Hyperion, Deimos, Phoebe, Quaoar加入至bikes
  </li>
  <li>
    查看bikes目前有多少基數(不重複元素)
  </li>
  <li>
    Salacia, Mimas, Quaoar加入至commuter_bikes
  </li>
  <li>
    將兩個key> bikes與commuter_bikes合併成一張表，命名為all_bikes
  </li>
  <li>
    查看all_bikes目前有多少基數
  </li>
</ol>

第4個操作不會將原本兩表刪除，還是會保留著。

如果想要HLL的資料刪除的話，可使用del與TTL時間到達後自行刪除

 [1]: https://redis.io/docs/data-types/probabilistic/hyperloglogs/