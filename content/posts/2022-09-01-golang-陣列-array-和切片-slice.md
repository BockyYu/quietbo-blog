---
title: '[Golang] 陣列 (array) 和切片 (slice)'
author: Bocky
type: post
date: 2022-08-31T19:07:12+00:00
url: /2022/09/01/golang-陣列-array-和切片-slice/
categories:
  - golang
tags:
  - golang

---
## 陣列 

陣列索引是從 0 開始, 以索引 (index) 對陣列賦值。  
附上Code:

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">package main

import "fmt"

func main() {

    fmt.Println("===一維數組===")
    //var
    var arr [3]int
    fmt.Println(arr[0])
    fmt.Println(len(arr))
    fmt.Println(arr[len(arr)-1])

    //for _, v := range arr{
    //  fmt.Printf("%d \n", v)
    //}
    for i, v := range arr {
        fmt.Printf("%d %d \n", i, v)
    }
    //0
    //3
    //0
    //0 0
    //1 0
    //2 0

    var arr1 [3]int = [3]int{1, 3, 5}
    fmt.Println(arr1[2]) //5

    arr2 := [...]int{1, 3, 5}
    fmt.Println(arr2[2]) //5

    fmt.Println(arr1 == arr2) //true

    for i, v := range arr2 {
        fmt.Printf("%d %d \n", i, v)
    }
    //0 1
    //1 3
    //2 5

    fmt.Println("===多維數組===")

    //var arr3 [4][2]int  //宣告方式
    arr3 := [4][2]int{{11, 22}, {12, 23}, {45, 62}, {83, 26}}
    fmt.Println(arr3[0][0]) //11
    fmt.Println(arr3[3][1]) //26
    //fmt.Println(arr3[4][2]) //超過會報錯

    fmt.Println("======")
    arr4 := [4][2]int{1: {11, 22}, 3: {31, 36}}
    fmt.Println(arr4[0][0]) //0
    fmt.Println(arr4[1][0]) //11
    fmt.Println(arr4[2][0]) //0
    fmt.Println(arr4[3][1]) //36

    fmt.Println("======")

    arr5 := [4][3]int{1: {0: 100}, 3: {2: 33}}
    fmt.Println(arr5[1][0]) //100
    fmt.Println(arr5[3][2]) //33
    fmt.Println(arr5[1][1]) //0

    arr5[1][1] = 66         //賦值
    fmt.Println(arr5[1][1]) //66
}</code></pre>

## 切片 

使用 make() 函數來創建切片:

<pre class="wp-block-code"><code class="">var slice1 []type = make([]type, len)
// 也可以簡寫為
slice1 := make([]type, len)
//slice11 := make([]int, len)</code></pre>

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">package main

import (
    "fmt"
)

func main() {

    //slice [開始位置:結束位置]
    var arr = [3]int{1, 2, 3}
    fmt.Println(arr, arr[1:2]) //[1 2 3] [2]

    var arr1 = [10]int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
    fmt.Println(arr1[2:5]) // [3 4 5]
    fmt.Println(arr1[:5])  //[1 2 3 4 5]

    fmt.Println(arr1[5:])  //[6 7 8 9 10]
    fmt.Println(arr1[:])   //[1 2 3 4 5 6 7 8 9 10]  //跟 [0:10], [:10]一樣
    fmt.Println(arr1[0:0]) //[0]

    //var name[]Type
    //var stringSlice []string
    //var numberSlice []int
    //var numberEmptySlice []int

    //make([]Type, size. cap)  // make 並不會回傳指標
    a := make([]int, 2)
    b := make([]int, 2, 10)
    fmt.Println(a, b) //[0 0] [0 0]
}</code></pre>

append 添加元素

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">package main

import (
    "fmt"
)

func main() {
    var a, b []int
    a = append(a, 1) // 追加一個元素
    fmt.Println(a)   //[1]

    b = append(b, 1, 2, 3) // 追加三個元素
    fmt.Println(b)         //[1 2 3]

    b = append(b, []int{4, 6, 8}...) // 從後方添加
    fmt.Println(b)                   //[1 2 3 4 6 8]

    var sli []int

    for i := 0; i &lt; 10; i++ {
        sli = append(sli, i)
        fmt.Printf("長度:%d,容量:%d,地址:%p\n", len(sli), cap(sli), sli)
    }
    //長度:1,容量:1,地址:0xc00000e128
    //長度:2,容量:2,地址:0xc00000e130
    //長度:3,容量:4,地址:0xc0000141e0
    //長度:4,容量:4,地址:0xc0000141e0
    //長度:5,容量:8,地址:0xc000012280
    //長度:6,容量:8,地址:0xc000012280
    //長度:7,容量:8,地址:0xc000012280
    //長度:8,容量:8,地址:0xc000012280
    //長度:9,容量:16,地址:0xc00010c000
    //長度:10,容量:16,地址:0xc00010c000

    var r = []int{1, 2, 3}
    r = append([]int{0}, r...) //從前面加了0
    fmt.Println(r)             //[0 1 2 3]

    r = append([]int{-4, -3, -2, -1}, r...)
    fmt.Println(r) //[-4 -3 -2 -1 0 1 2 3]
    //盡量不要從前面去加

    // 一般容量會大於長度
}</code></pre>

### copy 

copy() 可以將一個數組切片複製到另一個數組切片中，如果加入的兩個數組切片不一樣大，就會按照其中較小的那個數組切片的元素個數進行複制。

範例1:

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">package main

import (
    "fmt"
)

func main() {
    // copy(目標切片, 源切片)類型

    slice1 := []int{1, 2, 3, 4, 5, 6}
    slice2 := []int{7, 8, 9}
    slice3 := []int{9, 8, 7}
    //copy(slice1, slice2) //複製 7 8 9 到s1 的1 2 3 位置
    copy(slice1, slice2)
    fmt.Println(slice1) //[7 8 9 4 5 6]
    fmt.Println(slice2) //[7 8 9]
    fmt.Println("=========")
    // 與長度有關, 會將 7 8 9 複製到slice3
    copy(slice3, slice1)
    fmt.Printf("slice1:%d, slice3:%d \n", slice1, slice3)
    // slice1:[7 8 9 4 5 6], slice3:[7 8 9][7 8 9]

}</code></pre>

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">package main

import "fmt"

func main() {
    // copy(目標切片, 源切片)類型
    const len = 10 //const常量是一個簡單值的標識符，在程序運行時，不會被修改的量。
    //創建切片var slice1 []type = make([]type, len)
    slice11 := make([]int, len)
    for i := 0; i &lt; len; i++ {
        slice11[i] = i
    }
    slice33 := slice11
    slice22 := make([]int, len)
    copy(slice22, slice11)
    fmt.Println(slice11) //[0 1 2 3 4 5 6 7 8 9]
    fmt.Println(slice22) //[0 1 2 3 4 5 6 7 8 9]
    fmt.Println(slice33) //[0 1 2 3 4 5 6 7 8 9]

    slice11[0] = 999
    fmt.Println(slice11[0]) //999
    fmt.Println(slice22[0]) //0 不受影響
    fmt.Println(slice33[0]) //999

}</code></pre>

刪除元素

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">package main

import "fmt"

func main() {

    //刪除元素

    //方法
    var a = []int{1, 2, 3}
    a = a[2:]
    fmt.Println(a) //[3]

    //方法-append
    var b = []int{1, 2, 3, 4, 5, 6}
    fmt.Println(b[:1]) //[1]
    b = append(b[:1], b[4:]...)
    fmt.Println(b) //[1 5 6]

    //方法-copy
    var c = []int{1, 2, 3, 4, 5, 6, 7}
    c = c[:copy(c, c[3:])] // 與append類似
    fmt.Println(c)         // [4 5 6 7]

    //試者了解這取值的過程
    fmt.Println(c)              //[4 5 6 7 5 6 7]
    fmt.Println(c[3:])          //[4 5 6 7]
    fmt.Println(copy(c, c[3:])) //4
    fmt.Println(c[:4])          //[4 5 6 7]

    // 方法 - append
    var d = []int{1, 2, 3, 4, 5}
    fmt.Println(d[3+1:]) //[5]
    fmt.Println(d[:3])   //[1 2 3]
    // d = append(d[:N], d[N+1:]...)
    d = append(d[:3], d[3+1:]...)
    fmt.Println(d) //[1 2 3 5]

    // 方法 - copy
    var e = []int{1, 2, 3, 4, 5}
    e = e[:2+copy(e[2:], e[2+1:])]
    fmt.Println(e)//[1 2 4 5]

    //方法-slice

    slice1 := []int{1, 2, 3, 4, 5, 6, 7, 8}
    index := 2
    fmt.Println(slice1[:index], slice1[index+1:]) //[1 2] [4 5 6 7 8]

    slice1 = append(slice1[:index], slice1[index+1:]...)
    fmt.Println(slice1) //[1 2 4 5 6 7 8]

}</code></pre>