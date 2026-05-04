---
title: '[Mongodb] 資料內為什麼有$numberLong?(已解決)'
author: Bocky
type: post
date: 2023-03-10T16:56:40+00:00
url: /2023/03/11/mongodb-資料內為什麼有numberlong已解決/
categories:
  - MongoDB
  - Python

---
這件事情是不小心自己做了一個坑給自己踩的，  
我從公司的QAT測試環境的GUI(Mongodb compass)複製了一份data，內容複製出來如下:

```json
{
    "uuid" : "2580913",
    "name" : "UserName",
    "id" : "A123456789",
    "age" : 18,
    "weight" : 70,
    "height" : 175
    "birthday" :{
        "$numberLong" : "789798540000"
    }
    "registration_date": {
        "$numberLong": "1677211157126"
    }
}
```

然後在我自己本機用Studio 3T直接insert了這些相同格式的資料，都正常匯入了！ 後來我在local開發的時候find用了下方的方式來搜尋(注意!其實這是錯的，這裡的$numberLong是被當作層級使用)

```
{"birthday.$numberLong": {"$gte": "789798540000"}}
```

此時local能正常取出資料，我還沒意識到問題。 後來部署到QAT後頻繁出錯，一去了解才發現，原來當時從Mongodb compass複製出來的$numberLong該資料的type， 原始資料為:

```json
{
    "uuid" : "2580913068820",
    "name" : "UserName",
    "id" : "A123456789",
    "age" : 18,
    "weight" : 70,
    "height" : 175
    "birthday" : 789798540000,
    "registration_date": 1677211157126
}
```

我後來去QAT機器測了一下這段，(如果birthday的type是int)

```
db.user.find ({birthday:{$ type : "int" }})
```

結果沒有資料。我把int換成了long：

```
db.user.find ({birthday:{$ type : "long" }})
```

就出現一堆資料了。 其實我一開始在把QAT的測試資料存進local這裡就出錯了！ 原因是Mongodb compass在複製資料時為了區分int和long這兩個不同的type，所以加了$numberLong 這段讓我們肉眼能夠判斷資料的type，後來我把$numberLong都拿掉後，公司QAT就正常可以取得資料了。