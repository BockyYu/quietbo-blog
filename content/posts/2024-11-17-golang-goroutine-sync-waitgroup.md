---
title: '[Golang] goroutine & sync.WaitGroup'
author: Bocky
type: post
date: 2024-11-17T15:27:57+00:00
url: /2024/11/17/golang-goroutine-sync-waitgroup/
categories:
  - golang

---
</p> 

Goroutine 是 Go 語言中一種輕量級的並發執行單元。我們可以使用 Goroutine 來實現並發編程,提高程式的效率和性能。</p> 

sync.WaitGroup 是 Go 標準庫中提供的一個同步原語,它用於等待一組 Goroutine 全部執行完畢。我們可以通過以下方式使用 sync.WaitGroup:</p> 

創建 WaitGroup 實例:</p> 

<pre class="wp-block-code"><code class="">wg := new(sync.WaitGroup)</code></pre></p> 

使用 wg.Add(n) 可以將 WaitGroup 的計數器增加 n。每啟動一個新的 Goroutine,都需要增加計數器。  
增加 WaitGroup 計數器:</p> 

<pre class="wp-block-code"><code class="">wg.Add(n)</code></pre></p> 

等待所有 Goroutine 完成</p> 

<pre class="wp-block-code"><code class="">wg.Wait()</code></pre></p> 

在 main 函數中,使用 wg.Wait() 可以阻塞直到所有 Goroutine 都完成。</p> 

在 Goroutine 中減少計數器:</p> 

<pre class="wp-block-code"><code class="">defer wg.Done()</code></pre></p> 

在 Goroutine 內部,使用 defer wg.Done() 可以在 Goroutine 退出時,將 WaitGroup 的計數器減 1。</p> 

下方為實作的code，找質數：一般如果用for迴圈會非常慢</p> 

<pre class="wp-block-code"><code class="">package main

import (
    "fmt"
    "time"
)

func main() {
    num := 300000
    start := time.Now()
    for i := 1; i &lt;= num; i++ {
        if isPrime(i) {
            fmt.Println(i)
        }
    }
    end := time.Now()
    fmt.Println(end.Unix() - start.Unix(), "seconds")
}

func isPrime(num int) bool {
    if num == 1 {
        return false
    } else if num == 2 {
        return true
    } else {
        for i := 2; i &lt; num; i++ {
            if num % i == 0 {
                return false
            }
        }
        return true
    }
}</code></pre></p> 

單純只使用Goroutine，在使用findPrimes之前加go，會沒辦法知道實際到底花幾秒的時間，以及main時間到就會結束。  
main 啟動了 300000 個 Goroutine，每個 Goroutine 調用 findPrimes 函數。  
但是 main 函數並沒有等待所有 Goroutine 執行完畢,而是直接等待了 2 秒鐘輸出 done。  
單純使用 Goroutine 而不使用 sync.WaitGroup 或其他同步機制,無法確保所有任務都已完成,也無法準確測量總的執行時間。</p> 

<pre class="wp-block-code"><code class="">package main

import (
    "fmt"
    "time"
)

func main() {
    num := 300000
    for i := 1; i &lt;= num; i++ {
        go findPrimes(i)
    }
    time.Sleep(2 * time.Second)
    fmt.Println("done")
}

func findPrimes(num int) {
    if num == 1 {
        return
    } else if num == 2 {
        fmt.Println(num)
    } else {
        for i := 2; i &lt; num; i++ {
            if num % i == 0 {
                return
            }
        }
        fmt.Println(num)
    }
}</code></pre></p> 

因此,我們無法確定在 &#8220;done&#8221; 輸出之前,所有 findPrimes 函數都已經執行完畢，要解決這個問題,最簡單的方法就是使用 sync.WaitGroup。</p> 

下方正確使用了 sync.WaitGroup 來確保所有 Goroutine 都執行完畢,並且能夠正確地計算整個過程的耗時。</p> 

<pre class="wp-block-code"><code class="">package main

import (
    "fmt"
    "sync"
    "time"
)

func main() {
    wg := new(sync.WaitGroup)
    num := 300000
    wg.Add(num) // 設置需要檢查的數字範圍為 1 到 300000
    start := time.Now().Unix()
    for i := 1; i &lt;= num; i++ {
        go findPrimes(i, wg) // 啟動 num 個 goroutine,每個 goroutine 都調用 findPrimes 函數。

    }
    wg.Wait() // 在所有goroutine完成之前, main 函數會一直等待,使用 wg.Wait()
    end := time.Now().Unix()
    fmt.Print(end-start, "seconds")
}

func findPrimes(num int, wg *sync.WaitGroup) {
    defer wg.Done() // 確保在函數退出時,WaitGroup 的計數器會被減 1
    if num == 1 {
        return
    } else if num == 2 {
        fmt.Println(num)
    } else {
        for i := 2; i &lt; num; i++ {
            if num%i == 0 {
                return
            }
        }
        fmt.Println(num)
    }
}</code></pre></p>