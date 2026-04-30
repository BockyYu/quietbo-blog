---
title: '[Golang] go run: cannot run non-main package(解決)'
author: Bocky
type: post
date: 2022-08-08T08:39:55+00:00
url: /2022/08/08/golang-go-run-cannot-run-non-main-package解決/
categories:
  - golang
tags:
  - golang

---
寫了第一個go程序，很簡單，就是一個簡單的輸出語句，但是確報了  
go run: cannot run non-main package 的錯誤信息，代碼如下：

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">package example

import "fmt"

const englishHelloPrefix = "Hello, "

func Hello(name string) string {
    return englishHelloPrefix + name
}

func main() {
    fmt.Println(Hello("world"))
}</code></pre>

在終端機執行了main.go的檔案但出現錯誤

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">$ go run main.go 
go run: cannot run non-main package</code></pre>

main方法只能放在package main中，go run 是執行命令，必須要一個main用來調用

把第一行改成下方就可以了

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">package main</code></pre>