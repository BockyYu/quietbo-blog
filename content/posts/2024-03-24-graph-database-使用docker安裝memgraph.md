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
 

<ul class="wp-block-list">
  <li>
    使用docker desktop
  </li>
</ul>

``

## 什麼是 Graph database ？ {.wp-block-heading}

[Graph database簡稱GDB][1],是一個使用圖結構進行語意查詢的資料庫，它使用節點、邊和屬性來表示和儲存資料。 該系統的關鍵概念是圖，它直接將儲存中的資料項，與資料節點和節點間表示關係的邊的集合相關聯

目前有哪些GraphDB,排名:<a href="https://db-engines.com/en/ranking/graph+dbmsmemgraph" target="_blank" rel="noreferrer noopener">圖形資料庫排名</a>以及所有<a href="https://db-engines.com/en/ranking" target="_blank" rel="noreferrer noopener">受歡迎程度對資料庫管理系統進行排名</a>

## docker desktop 安裝 memgraph {.wp-block-heading}<figure class="wp-block-image size-large">

<img loading="lazy" decoding="async" width="1024" height="579" src="https://quietbo.com/wp-content/uploads/2024/03/image-1-1024x579.png" alt="" class="wp-image-1030" srcset="https://quietbo.com/wp-content/uploads/2024/03/image-1-1024x579.png 1024w, https://quietbo.com/wp-content/uploads/2024/03/image-1-300x170.png 300w, https://quietbo.com/wp-content/uploads/2024/03/image-1-768x434.png 768w, https://quietbo.com/wp-content/uploads/2024/03/image-1.png 1266w" sizes="auto, (max-width: 1024px) 100vw, 1024px" /> </figure> 

以在 localhost:7687 看到 memgraph 的介面了。<figure class="wp-block-image size-large">

<img loading="lazy" decoding="async" width="1024" height="551" src="https://quietbo.com/wp-content/uploads/2024/03/image-2-1024x551.png" alt="" class="wp-image-1031" srcset="https://quietbo.com/wp-content/uploads/2024/03/image-2-1024x551.png 1024w, https://quietbo.com/wp-content/uploads/2024/03/image-2-300x161.png 300w, https://quietbo.com/wp-content/uploads/2024/03/image-2-768x413.png 768w, https://quietbo.com/wp-content/uploads/2024/03/image-2-1536x827.png 1536w, https://quietbo.com/wp-content/uploads/2024/03/image-2-2048x1102.png 2048w" sizes="auto, (max-width: 1024px) 100vw, 1024px" /> </figure> <figure class="wp-block-image size-large"><img loading="lazy" decoding="async" width="1024" height="638" src="https://quietbo.com/wp-content/uploads/2024/03/image-3-1024x638.png" alt="" class="wp-image-1032" srcset="https://quietbo.com/wp-content/uploads/2024/03/image-3-1024x638.png 1024w, https://quietbo.com/wp-content/uploads/2024/03/image-3-300x187.png 300w, https://quietbo.com/wp-content/uploads/2024/03/image-3-768x478.png 768w, https://quietbo.com/wp-content/uploads/2024/03/image-3-1536x956.png 1536w, https://quietbo.com/wp-content/uploads/2024/03/image-3-2048x1275.png 2048w" sizes="auto, (max-width: 1024px) 100vw, 1024px" /></figure> 

點擊左方的Datasets 找 CORA: Scientific publications classified into seven categories<figure class="wp-block-image size-large">

<img loading="lazy" decoding="async" width="1024" height="550" src="https://quietbo.com/wp-content/uploads/2024/03/image-4-1024x550.png" alt="" class="wp-image-1033" srcset="https://quietbo.com/wp-content/uploads/2024/03/image-4-1024x550.png 1024w, https://quietbo.com/wp-content/uploads/2024/03/image-4-300x161.png 300w, https://quietbo.com/wp-content/uploads/2024/03/image-4-768x413.png 768w, https://quietbo.com/wp-content/uploads/2024/03/image-4-1536x826.png 1536w, https://quietbo.com/wp-content/uploads/2024/03/image-4.png 1920w" sizes="auto, (max-width: 1024px) 100vw, 1024px" /> </figure> 

  
執行完成後點擊 run query<figure class="wp-block-image size-large">

<img loading="lazy" decoding="async" width="1024" height="550" src="https://quietbo.com/wp-content/uploads/2024/03/image-5-1024x550.png" alt="" class="wp-image-1034" srcset="https://quietbo.com/wp-content/uploads/2024/03/image-5-1024x550.png 1024w, https://quietbo.com/wp-content/uploads/2024/03/image-5-300x161.png 300w, https://quietbo.com/wp-content/uploads/2024/03/image-5-768x413.png 768w, https://quietbo.com/wp-content/uploads/2024/03/image-5-1536x826.png 1536w, https://quietbo.com/wp-content/uploads/2024/03/image-5.png 1920w" sizes="auto, (max-width: 1024px) 100vw, 1024px" /> </figure> 

  
會出現下方成功的結果<figure class="wp-block-image size-large">

<img loading="lazy" decoding="async" width="1024" height="591" src="https://quietbo.com/wp-content/uploads/2024/03/image-1024x591.png" alt="" class="wp-image-1027" srcset="https://quietbo.com/wp-content/uploads/2024/03/image-1024x591.png 1024w, https://quietbo.com/wp-content/uploads/2024/03/image-300x173.png 300w, https://quietbo.com/wp-content/uploads/2024/03/image-768x443.png 768w, https://quietbo.com/wp-content/uploads/2024/03/image.png 1355w" sizes="auto, (max-width: 1024px) 100vw, 1024px" /> </figure> 

## Python連線 {.wp-block-heading}

<ul class="wp-block-list">
  <li>
    使用pycharm
  </li>
</ul>

官網教學:[網址][2]

當memgraph建立成功後使用下方程式碼來建立Person

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">import mgclient

conn = mgclient.connect(host='127.0.0.1', port=7687)
cursor = conn.cursor()
cursor.execute("""
        CREATE (n:Person {name: 'John'})-[e:KNOWS]-&gt;
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
conn.close()</code></pre>

接著在memgraph下sql指令即可看到剛才創建的2筆資料

<pre class="wp-block-code"><code lang="sql" class="language-sql">MATCH (c:Person) RETURN c;</code></pre>

 [1]: https://zh.wikipedia.org/zh-tw/%E5%9B%BE%E6%95%B0%E6%8D%AE%E5%BA%93
 [2]: https://pypi.org/project/pymgclient/0.1.0/