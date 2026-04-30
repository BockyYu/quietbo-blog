---
title: '[Python] pymysql.err.IntegrityError 解決'
author: Bocky
type: post
date: 2022-04-15T03:19:05+00:00
url: /2022/04/15/python-pymysql-err-integrityerror-解決/
categories:
  - Python
tags:
  - python

---
通常遇到這狀況代表有設定unique的欄位, 被重複了,  
而且要新增的一筆資料又與該欄位有重複的值,則會報錯,

假設我的欄位id已經有202204150012的資料時, 要再增加一筆id是202204150012的資料, 錯誤訊息如下, 會告知是哪個欄位重複與重複的value

<pre class="wp-block-code"><code lang="bash" class="language-bash">(pymysql.err.IntegrityError) (1062, "Duplicate entry '202204150012' for key 'tb_order.id'")</code></pre>

解決方式1:  
將該欄位的unique拿掉

解決方式2:  
做異常處理與回滾(rollback)

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">try:
    db.commit()
except:
    # 回滾
    db.rollback()
finally:
# 關閉數據庫連接
db.close()</code></pre>

<pre class="wp-block-preformatted">解決方式3:例外處理時跳過</pre>

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">try:
    .... 
except IntegrityError as error:
    # 獨立處理重複
    result1 = re.search('Duplicate entry', str(error))
    if result1:
        logger.error('Duplicate entry')
        pass
except Exception as error:
    # 其他例外處理 ...
    </code></pre>