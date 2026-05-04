---
title: '[Python] 有序的Dict – OrderedDict (必學)'
author: Bocky
type: post
date: 2021-07-21T17:00:01+00:00
url: /2021/07/22/python-有序的dict-ordereddict-必學/
categories:
  - Python
tags:
  - python

---
特性:**依據key被插入的先後做排序，如果更新了某個key的值，不會影響排序位置，除非是把key刪除後又重新插入。後續加入的key都會從最末做添加**。  
本篇沒做增刪查改的範例。

## dict(一般常用的) 

一般常用的dict都會說是無序，但其實還是有一定的順序，是**按照hash來存儲的，和存儲的數據結構有關**(本篇不多說明)，但通常這個跟我們一般認真的序列有一點不一樣，因為不是填入時的順序。

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">example_dict = dict(
    name='Bocky',
    phone='0912-345-678',
    address='Taiwan-Taipei',
    age='18'
)
print(example_dict)</code></pre>

輸出結果:

<pre class="wp-block-code"><code lang="" class=" line-numbers">{'phone': '0912-345-678', 'age': '18', 'name': 'Bocky', 'address': 'Taiwan-Taipei'}</code></pre>

## OrderedDict 

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers">from collections import OrderedDict
import json
# 錯誤示範，沒有照順序排列的效果(與一般dict結果一樣)
example_ordered_dict_0 = OrderedDict(
    name='Bocky',
    phone='0912-345-678',
    address='Taiwan-Taipei',
    age='18'
)
print('錯誤示範的輸出:\n{}'.format(example_ordered_dict_0))
print("="*20)

example_ordered_dict_1 = OrderedDict([
    ('name', 'Bocky'),
    ('phone_number', '0912-345-678'),
    ('address', 'Taiwan-Taipei'),
    ('age', '18')
])
print("OrderedDict輸出結果:\n{}".format(example_ordered_dict_1))
print("="*20)

print("添加一個key為interest到最末端:")
example_ordered_dict_1['interest'] = 'sleep'
print(example_ordered_dict_1)
print("="*20)

print("把OrderedDict轉成字串,並剔除空白:")
print (json.dumps(example_ordered_dict_1).replace(" ", ""))</code></pre>

輸出結果:

<pre class="wp-block-code"><code lang="" class=" line-numbers">錯誤示範的輸出:
OrderedDict([('phone', '0912-345-678'), ('age', '18'), ('name', 'Bocky'), ('address', 'Taiwan-Taipei')])
====================
OrderedDict輸出結果:
OrderedDict([('name', 'Bocky'), ('phone_number', '0912-345-678'), ('address', 'Taiwan-Taipei'), ('age', '18')])
====================
添加一個key為interest到最末端:
OrderedDict([('name', 'Bocky'), ('phone_number', '0912-345-678'), ('address', 'Taiwan-Taipei'), ('age', '18'), ('interest', 'sleep')])
====================
把OrderedDict轉成字串,並剔除空白:
{"name":"Bocky","phone_number":"0912-345-678","address":"Taiwan-Taipei","age":"18","interest":"sleep"}</code></pre>

如果是要a~z排序的話就使用sorted，網路上很多參考，但這就不需要使用OrderedDict了，一般dict就可以做到，只是排序拼接而已，我自己工作上是很常用:

<pre class="wp-block-code"><code lang="" class=" line-numbers">data = "&".join("{0}={1}".format(str(k), str(example_ordered_dict_1[k])) for k in sorted(example_ordered_dict_1.keys()))</code></pre>

輸出結果:

<pre class="wp-block-code"><code lang="" class="">address=Taiwan-Taipei&age=18&interest=sleep&name=Bocky&phone_number=0912-345-678</code></pre>