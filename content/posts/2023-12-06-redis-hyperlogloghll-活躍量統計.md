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

```
基數: 不重複元素, 例如{1, 2, 3, 5, 5, 5, 6}, 基數集為{1, 2, 3, 5, 6}, 基數為5;
```

本次範例使用Docker內建立一個Redis容器 \[Redis-hyperloglogs\]\[1\] HyperLogLogs 提供了3個指令：

*   pfadd : 添加
*   pfcount : 計數
*   pfmerge : 合併

```
> PFADD bikes Hyperion Deimos Phoebe Quaoar
(integer) 1
> PFCOUNT bikes
(integer) 4
> PFADD commuter_bikes Salacia Mimas Quaoar
(integer) 1
> PFMERGE all_bikes bikes commuter_bikes
OK
> PFCOUNT all_bikes
(integer) 6
```

以上的操作說明為:

1.  將Hyperion, Deimos, Phoebe, Quaoar加入至bikes
2.  查看bikes目前有多少基數(不重複元素)
3.  Salacia, Mimas, Quaoar加入至commuter\_bikes
4.  將兩個key> bikes與commuter\_bikes合併成一張表，命名為all\_bikes
5.  查看all\_bikes目前有多少基數

第4個操作不會將原本兩表刪除，還是會保留著。 如果想要HLL的資料刪除的話，可使用del與TTL時間到達後自行刪除 \[1\]: https://redis.io/docs/data-types/probabilistic/hyperloglogs/