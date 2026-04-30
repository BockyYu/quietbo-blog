---
title: '[Golang] 接口interface'
author: Bocky
type: post
date: 2022-09-10T15:10:52+00:00
url: /2022/09/10/golang-接口interface/
categories:
  - golang
tags:
  - golang

---
<pre class="wp-block-code"><code class="">type 類型名 struct{
    字段1 類型
    字段2 類型
}

定義接口
type interface_name interface{
    方法名 method_name1
    方法名 method_name2
    ....
}

定義結構體
type struct_name struct{

}


func(struct_name_var struct_name) method_name1() [返回類型]{
    //方法實現
}


func(struct_name_var struct_name) method_nam2() [返回類型]{
    //方法實現
}</code></pre>

範例:

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">package main

import "fmt"


type Mobile interface {
    call()
    message()
}

type Iphone struct {
}

type Samsung struct{
}

func (iphone13 Iphone) call(){
    fmt.Println("iphone13, call phone number")
}

func (iphone13 Iphone) message(){
    fmt.Println("iphone13, use message")
}

func (s22 Samsung) call(){
    fmt.Println("samsung, call phone number")
}

func (s22 Samsung) message(){
    fmt.Println("samsung, use message")
}

func main() {
    var mobile Mobile
    mobile=new(Iphone)
    mobile.call()
    mobile.message()


    var mobile2 Mobile
    mobile2=new(Samsung)
    mobile2.call()
    mobile2.message()
}</code></pre>

顯示

<pre class="wp-block-code"><code class=" line-numbers">iphone13, call phone number
iphone13, use message
samsung, call phone number
samsung, use message</code></pre>

## 空接口類型 {.wp-block-heading}

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">package main

import (
    "fmt"
)

func main() {
    var any interface{}
    any = 100
    fmt.Printf("value:%d type:%T \n", any, any)

    any = "aaa"
    fmt.Printf("value:%s type:%T \n", any, any)

    testFunc(100)
    testFunc("test")
}

func testFunc(par interface{}){
    fmt.Println(par)
}</code></pre>

<pre class="wp-block-code"><code class=" line-numbers">value:100 type:int 
value:aaa type:string 
100
test</code></pre>