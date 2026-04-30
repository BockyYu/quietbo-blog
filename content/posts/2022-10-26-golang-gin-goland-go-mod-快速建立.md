---
title: '[Golang] Gin & Goland & go.mod 快速建立'
author: Bocky
type: post
date: 2022-10-25T17:49:24+00:00
url: /2022/10/26/golang-gin-goland-go-mod-快速建立/
categories:
  - golang
  - 程式語言
tags:
  - golang

---
打開Goland後main.go檔內複製下方的Code:

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">package main

import (
    "github.com/gin-gonic/gin"
)
func main() {
    app := gin.Default()
    app.GET("/hello/:name", func(c *gin.Context) {
        name := c.Param("name")
        c.JSON(200, gin.H{
            "message": "hello " + name,
        })
    })
    err := app.Run(":8080")
    if err != nil {
        panic(err)
    }
}</code></pre>

會看到很多紅字如下圖  
<img decoding="async" src="https://i.imgur.com/CaqIcVr.png" alt="" /> 

打開Goland的file -> settings -> Go Modules ->  
將Enable Go modules integration打勾  
<img decoding="async" src="https://i.imgur.com/CCEOu0Z.png" alt="" /> 

再Goland下方打開terminal，輸入

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">$ go mod init [project_name]
$ go mod tidy</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/pn7NIKz.png" alt="" /> </figure> 

此時的go.mod會自動下載

<pre class="wp-block-code"><code class="">module do_gowork

go 1.19

require github.com/gin-gonic/gin v1.8.1

require (
    github.com/gin-contrib/sse v0.1.0 // indirect
    github.com/go-playground/locales v0.14.0 // indirect
    github.com/go-playground/universal-translator v0.18.0 // indirect
    github.com/go-playground/validator/v10 v10.10.0 // indirect
    github.com/goccy/go-json v0.9.7 // indirect
    github.com/json-iterator/go v1.1.12 // indirect
    github.com/leodido/go-urn v1.2.1 // indirect
    github.com/mattn/go-isatty v0.0.14 // indirect
    github.com/modern-go/concurrent v0.0.0-20180228061459-e0a39a4cb421 // indirect
    github.com/modern-go/reflect2 v1.0.2 // indirect
    github.com/pelletier/go-toml/v2 v2.0.1 // indirect
    github.com/ugorji/go/codec v1.2.7 // indirect
    golang.org/x/crypto v0.0.0-20210711020723-a769d52b0f97 // indirect
    golang.org/x/net v0.0.0-20210226172049-e18ecbb05110 // indirect
    golang.org/x/sys v0.0.0-20210806184541-e5e7981a1069 // indirect
    golang.org/x/text v0.3.6 // indirect
    google.golang.org/protobuf v1.28.0 // indirect
    gopkg.in/yaml.v2 v2.4.0 // indirect
)</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/AE6i33f.png" alt="" /> </figure> 

注意，go mod tidy有移除「沒使用的依賴這功能」，實際上是需要使用來取得library。

<pre class="wp-block-code"><code class="">go get [library]</code></pre>

空白處點選右鍵，Run &#8216;go build main.go&#8217;<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/fw3ni1J.png" alt="" /> </figure> 

執行成功可看到下面這些訊息

<pre class="wp-block-code"><code class="">[GIN-debug] [WARNING] Creating an Engine instance with the Logger and Recovery middleware already attached.

[GIN-debug] [WARNING] Running in "debug" mode. Switch to "release" mode in production.
 - using env:    export GIN_MODE=release
 - using code:    gin.SetMode(gin.ReleaseMode)

[GIN-debug] GET    /hello/:name              --&gt; main.main.func1 (3 handlers)
[GIN-debug] [WARNING] You trusted all proxies, this is NOT safe. We recommend you to set a value.
Please check https://pkg.go.dev/github.com/gin-gonic/gin#readme-don-t-trust-all-proxies for details.
[GIN-debug] Listening and serving HTTP on :8080</code></pre>

打開瀏覽器輸入:  
http://127.0.0.1:8080/hello/world

{&#8220;message&#8221;:&#8221;hello world&#8221;}