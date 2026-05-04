---
author: Bocky
type: post
date: 2022-09-12T14:41:24+00:00
url: /2022/09/12/golang-goroutine-channel/
categories:
  - golang
tags:
  - golang

---
<div id="ez-toc-container" class="ez-toc-v2_0_82_2 ez-toc-wrap-center counter-hierarchy ez-toc-counter ez-toc-grey ez-toc-container-direction">
  <div class="ez-toc-title-container">
    <p class="ez-toc-title" style="cursor:inherit">
      Table of Contents
    </p>
    
    <span class="ez-toc-title-toggle"><a href="#" class="ez-toc-pull-right ez-toc-btn ez-toc-btn-xs ez-toc-btn-default ez-toc-toggle" aria-label="顯示/隱藏內容目錄"><span class="ez-toc-js-icon-con"><span class=""><span class="eztoc-hide" style="display:none;">Toggle</span><span class="ez-toc-icon-toggle-span"><svg style="fill: #999;color:#999" xmlns="http://www.w3.org/2000/svg" class="list-377408" width="20px" height="20px" viewBox="0 0 24 24" fill="none"><path d="M6 6H4v2h2V6zm14 0H8v2h12V6zM4 11h2v2H4v-2zm16 0H8v2h12v-2zM4 16h2v2H4v-2zm16 0H8v2h12v-2z" fill="currentColor"></path></svg><svg style="fill: #999;color:#999" class="arrow-unsorted-368013" xmlns="http://www.w3.org/2000/svg" width="10px" height="10px" viewBox="0 0 24 24" version="1.2" baseProfile="tiny"><path d="M18.2 9.3l-6.2-6.3-6.2 6.3c-.2.2-.3.4-.3.7s.1.5.3.7c.2.2.4.3.7.3h11c.3 0 .5-.1.7-.3.2-.2.3-.5.3-.7s-.1-.5-.3-.7zM5.8 14.7l6.2 6.3 6.2-6.3c.2-.2.3-.5.3-.7s-.1-.5-.3-.7c-.2-.2-.4-.3-.7-.3h-11c-.3 0-.5.1-.7.3-.2.2-.3.5-.3.7s.1.5.3.7z"/></svg></span></span></span></a></span>
  </div><nav>
  
  <ul class='ez-toc-list ez-toc-list-level-1 ' >
    <li class='ez-toc-page-1 ez-toc-heading-level-1'>
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2022/09/12/golang-goroutine-channel/#Golang_goroutine_channel" >[Golang] goroutine & channel</a><ul class='ez-toc-list-level-2' >
        <li class='ez-toc-heading-level-2'>
          <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2022/09/12/golang-goroutine-channel/#Channel" >Channel</a><ul class='ez-toc-list-level-3' >
            <li class='ez-toc-heading-level-3'>
              <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2022/09/12/golang-goroutine-channel/#%E9%A1%9E%E5%9E%8B%E8%88%87%E5%89%B5%E5%BB%BA" >類型與創建</a>
            </li>
            <li class='ez-toc-page-1 ez-toc-heading-level-3'>
              <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2022/09/12/golang-goroutine-channel/#%E7%99%BC%E9%80%81%E8%88%87%E6%8E%A5%E6%94%B6" >發送與接收</a>
            </li>
          </ul>
        </li>
        
        <li class='ez-toc-page-1 ez-toc-heading-level-2'>
          <a class="ez-toc-link ez-toc-heading-5" href="https://quietbo.com/2022/09/12/golang-goroutine-channel/#select" >select</a><ul class='ez-toc-list-level-3' >
            <li class='ez-toc-heading-level-3'>
              <a class="ez-toc-link ez-toc-heading-6" href="https://quietbo.com/2022/09/12/golang-goroutine-channel/#%E5%9F%BA%E6%9C%AC%E8%AA%9E%E6%B3%95" >基本語法</a>
            </li>
          </ul>
        </li>
      </ul>
    </li>
  </ul></nav>
</div>

# <span class="ez-toc-section" id="Golang_goroutine_channel"></span>[Golang] goroutine & channel<span class="ez-toc-section-end"></span> 

<ul class="wp-block-list">
  <li>
    Go <a href="https://www.runoob.com/go/go-concurrent.html">併發&通道（channel）</a>
  </li>
</ul>

## <span class="ez-toc-section" id="Channel"></span>Channel<span class="ez-toc-section-end"></span> 

Channel 是 Go 語言中用於 goroutine 之間通信的管道，是 Go 並發編程模型的核心組件之一。  
基本概念  
Channel 提供了一種 goroutine 之間的通信機制，使一個 goroutine 可以向另一個 goroutine 發送數據，而無需顯式的鎖或條件變量。

### <span class="ez-toc-section" id="%E9%A1%9E%E5%9E%8B%E8%88%87%E5%89%B5%E5%BB%BA"></span>類型與創建<span class="ez-toc-section-end"></span> 

<pre class="wp-block-code"><code class="">// 創建不同類型的 channel
ch1 := make(chan int)         // 無緩衝的整數 channel
ch2 := make(chan string, 10)  // 有 10 個緩衝區的字符串 channel
ch3 := make(chan interface{}) // 任意類型的 channel</code></pre>

### <span class="ez-toc-section" id="%E7%99%BC%E9%80%81%E8%88%87%E6%8E%A5%E6%94%B6"></span>發送與接收<span class="ez-toc-section-end"></span> 

<pre class="wp-block-code"><code class="">// 發送數據
ch &lt;- value

// 接收數據
value := &lt;-ch
value, ok := &lt;-ch  // ok 表示 channel 是否已關閉</code></pre>

goroutine + Channel 範例:

<pre class="wp-block-code"><code class="">package main
import "fmt"
import "time"
func main() {
    ch1 := make(chan int, 1)
    ch2 := make(chan string, 1)
    ch3 := make(chan interface{}, 1)

    ch1 &lt;- 1  // ch1 緩衝區已滿

    // 創建 goroutine 來接收第一個值
    go func() {
        time.Sleep(2 * time.Second)  // 等待1秒
        fmt.Println(&lt;-ch1)  // 1，此時釋放 ch1 的空間
    }()

    ch1 &lt;- 3  // 這裡會阻塞，直到上面的 goroutine 從 ch1 接收數據
    // 由於上面的 goroutine 有2秒延遲，這里會等待約2秒

    ch2 &lt;- "name"
    ch3 &lt;- "hi"

    fmt.Println(&lt;-ch1)  // 3
    fmt.Println(&lt;-ch2)  // "name"
    fmt.Println(&lt;-ch3)  // "hi"
}</code></pre>

顯示如下:

<pre class="wp-block-code"><code class="">1
3
name
hi</code></pre>

<ol start="2" class="wp-block-list">
  <li>
    範例&說明
  </li>
</ol>

<pre class="wp-block-code"><code class="">package main
import "fmt"

func main() {
    // 創建通道
    c := make(chan int)

    //併發執行
    go ifunc(c)
    for i := 1; i &lt;= 10; i++{
        // 將數據i發送給通道
        c &lt;- i
    }

    // 通道ifunc結束讀取數據
    c&lt;- 100

    //等於ifunc結束
    fmt.Println(&lt;-c)
}

func ifunc(c chan int) {

    // 阻塞等待數據
    for {
        //從通道獲取一個數據
        data := &lt;- c

        // 當取得的數據為100則結束阻塞
        if data == 100{
            break
        }
        // 輸出數據
        fmt.Println(data)
    }
    // 通知main結束
    c&lt;-0
}</code></pre>

output:

<pre class="wp-block-code"><code class="">1
2
3
4
5
6
7
8
9
10
0</code></pre>

補充:  
可以在  
fmt.Println(<-c)與fmt.Println(data)之前，print隨便一個數值，  
就可以看到，輸出模式取決於 Go 調度器如何在這兩個 goroutine 之間切換

## <span class="ez-toc-section" id="select"></span>select<span class="ez-toc-section-end"></span> 

select 是 Go 語言中的一個控制結構，專門用於處理多個通道操作。它的主要用途是同時等待多個通道的操作（發送或接收），並在其中一個操作可以進行時執行對應的代碼。

### <span class="ez-toc-section" id="%E5%9F%BA%E6%9C%AC%E8%AA%9E%E6%B3%95"></span>基本語法<span class="ez-toc-section-end"></span> 

<pre class="wp-block-code"><code class="">select {
case &lt;-chan1:
    // 從 chan1 接收到數據時執行
case chan2 &lt;- value:
    // 向 chan2 發送數據成功時執行
case x := &lt;-chan3:
    // 從 chan3 接收到數據並賦值給 x 時執行
default:
    // 沒有通道操作就緒時執行（非阻塞模式）
}</code></pre>

[select][1]

<pre class="wp-block-code"><code class="">package main

import (
    "fmt"
    "time"
)

func main() {
    // 創建兩個通道
    ch1 := make(chan string)
    ch2 := make(chan string)

    // 在一個 goroutine 中，1秒後發送數據到 ch1
    go func() {
        time.Sleep(1 * time.Second)
        ch1 &lt;- "來自通道1的數據"
    }()
    go func() {
        time.Sleep(1 * time.Second)
        ch1 &lt;- "來自通道1-1的數據"
    }()
    // 在另一個 goroutine 中，2秒後發送數據到 ch2
    go func() {
        time.Sleep(2 * time.Second)
        ch2 &lt;- "來自通道2的數據"
    }()

    go func() {
        time.Sleep(2 * time.Second)
        ch2 &lt;- "來自通道2-1的數據"
    }()

    // 使用 select 監聽兩個通道
    for i := 0; i &lt; 4; i++ {
        select {
        case msg1 := &lt;-ch1:
            fmt.Println("接收到:", msg1)
        case msg2 := &lt;-ch2:
            fmt.Println("接收到:", msg2)
        case &lt;-time.After(3 * time.Second):
            fmt.Println("操作超時")
        }
    }
}</code></pre>

output:

<pre class="wp-block-code"><code class="">接收到: 來自通道1-1的數據
接收到: 來自通道1的數據
接收到: 來自通道2的數據
接收到: 來自通道2-1的數據</code></pre>

 [1]: https://www.runoob.com/go/go-select-statement.html