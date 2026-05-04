---
title: '[Graph database] 使用docker安裝memgraph & python簡易連線'
author: Bocky
type: post
date: 2024-03-24T06:42:36+00:00
url: /2024/03/24/graph-database-使用docker安裝memgraph/
categories:
  - Graph
  - Python
tags:
  - graph
  - memgraph

---

*   使用docker desktop

## 什麼是 Graph database ？ 
\[Graph database簡稱GDB\]\[1\],是一個使用圖結構進行語意查詢的資料庫，它使用節點、邊和屬性來表示和儲存資料。 該系統的關鍵概念是圖，它直接將儲存中的資料項，與資料節點和節點間表示關係的邊的集合相關聯 目前有哪些GraphDB,排名:[圖形資料庫排名](https://db-engines.com/en/ranking/graph+dbmsmemgraph)以及所有[受歡迎程度對資料庫管理系統進行排名](https://db-engines.com/en/ranking) ## docker desktop 安裝 memgraph![](/uploads/2024/03/image-1-1024x579.png)以在 localhost:7687 看到 memgraph 的介面了。![](/uploads/2024/03/image-2-1024x551.png)![](/uploads/2024/03/image-3-1024x638.png)點擊左方的Datasets 找 CORA: Scientific publications classified into seven categories![](/uploads/2024/03/image-4-1024x550.png)執行完成後點擊 run query![](/uploads/2024/03/image-5-1024x550.png)會出現下方成功的結果![](/uploads/2024/03/image-1024x591.png)\## Python連線

*   使用pycharm

官網教學:\[網址\]\[2\] 當memgraph建立成功後使用下方程式碼來建立Person

```python
import mgclient

conn = mgclient.connect(host='127.0.0.1', port=7687)
cursor = conn.cursor()
cursor.execute("""
        CREATE (n:Person {name: 'John'})-[e:KNOWS]->
               (m:Person {name: 'Steve'})
        RETURN n, e, m
    """)

row = cursor.fetchone()
print(row[0])  # (:Person {'name': 'John'})
print(row[1])  # [:KNOWS]
print(row[2])  # (:Person {'name': 'Steve'})

conn.commit()  # 提交數據(沒有commit就不會真正存進資料庫內)
# 關閉游標和連線
cursor.close()
conn.close()
```

接著在memgraph下sql指令即可看到剛才創建的2筆資料

```sql
MATCH (c:Person) RETURN c;
```

\[1\]: https://zh.wikipedia.org/zh-tw/%E5%9B%BE%E6%95%B0%E6%8D%AE%E5%BA%93 \[2\]: https://pypi.org/project/pymgclient/0.1.0/