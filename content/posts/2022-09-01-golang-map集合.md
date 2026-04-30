---
title: '[Golang] map'
author: Bocky
type: post
date: 2022-09-01T08:30:28+00:00
url: /2022/09/01/golang-map集合/
categories:
  - golang
tags:
  - golang

---
宣告方式:

var name map[keyType]valueType

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">var map1 map[string]int

// 使用 make 建立 Map。
// Key 的型別是 string，Value 是 int
map2 := make(map[string]int)</code></pre>



賦值與刪除

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">package main

import "fmt"

func main() {
    // map 無序的鍵, 無法決定它的返回順序。通過key來檢索數據

    //var name map[keyType]valueType

    var map1 map[string]int
    map1 = map[string]int{"A": 1, "B": 2}
    fmt.Println(map1["B"]) //2
    //map1["C"] = "3" //會報錯

    map2 := make(map[string]float32)
    map2["k1"] = 2.345
    map2["k2"] = 1.3
    fmt.Println(map2["k1"]) // 2.345

    // 提前指定空間
    //map3 := make(map[string]int, 10)

    for k, v := range map1 {
        fmt.Println(k, v)
        //A 1
        //B 2
    }

    // 刪除方式
    // delete(map, key)
    delete(map2, "k1")
    for k, v := range map2 {
        fmt.Println(k, v)
        //k2 1.3
    }

}</code></pre>