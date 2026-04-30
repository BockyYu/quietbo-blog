---
title: '[Golang] List'
author: Bocky
type: post
date: 2022-09-01T09:44:37+00:00
url: /2022/09/01/golang-list/
categories:
  - golang
tags:
  - golang

---
List由多個節點所組成的, 節點之間透過一些變數紀錄彼此的關係

<pre class="wp-block-code"><code class="">a -&gt; next -&gt; b -&gt; next -&gt; c
a &lt;- pre &lt;- b &lt;- pre &lt;- c</code></pre>

宣告方式

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">name:=list.New()
//var name list.List</code></pre>

<ul class="wp-block-list">
  <li>
    PushBack:插入元素直接放入結尾
  </li>
  <li>
    PushFront:插入元素直接放入開頭
  </li>
  <li>
    InsertBefore:被標記的元素前增加元素
  </li>
  <li>
    InsertAfter:被標記的元素後增加元素
  </li>
</ul>

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">package main

import (
    "container/list"
    "fmt"
)

func main() {
    //List




    list1 := list.New()
    list1.PushBack("Back_1") //插入元素直接放入結尾
    list1.PushFront(111)     //插入元素直接放入最前   111 Back_1
    list1.PushBack("Back_2") //插入元素直接放入結尾 111 Back_1 Back_2

    el := list1.PushBack("Back_3") // 111 Back_1 Back_2 Back_3
    //在Back_3的後方加入After
    list1.InsertAfter("After", el) // 111 Back_1 Back_2 Back_3 After
    // 在Back_3的前方加入Before
    list1.InsertBefore("Before", el) // 111 Back_1 Back_2 Before Back_3 After

    // 移除 Back_3
    //list1.Remove(el)
    for i := list1.Front(); i != nil; i = i.Next() {
        fmt.Println(i.Value)
    }

}</code></pre>

顯示結果

<pre class="wp-block-code"><code class=" line-numbers">111
Back_1
Back_2
Before
Back_3
After</code></pre>