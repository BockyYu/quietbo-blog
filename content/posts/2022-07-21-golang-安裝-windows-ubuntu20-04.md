---
title: '[Golang] 安裝 (Windows & ubuntu20.04)'
author: Bocky
type: post
date: 2022-07-21T15:59:38+00:00
url: /2022/07/21/golang-安裝-windows-ubuntu20-04/
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
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-1" href="https://quietbo.com/2022/07/21/golang-%e5%ae%89%e8%a3%9d-windows-ubuntu20-04/#Windows%E5%AE%89%E8%A3%9D" >Windows安裝</a><ul class='ez-toc-list-level-3' >
        <li class='ez-toc-heading-level-3'>
          <a class="ez-toc-link ez-toc-heading-2" href="https://quietbo.com/2022/07/21/golang-%e5%ae%89%e8%a3%9d-windows-ubuntu20-04/#%E5%9F%B7%E8%A1%8C%E7%AC%AC%E4%B8%80%E6%94%AF%E7%A8%8B%E5%BC%8Fhellogo" >執行第一支程式hello.go</a>
        </li>
      </ul>
    </li>
    
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-3" href="https://quietbo.com/2022/07/21/golang-%e5%ae%89%e8%a3%9d-windows-ubuntu20-04/#ubuntu_%E5%AE%89%E8%A3%9D_golang_118" >[ubuntu] 安裝 golang 1.18</a><ul class='ez-toc-list-level-3' >
        <li class='ez-toc-heading-level-3'>
          <a class="ez-toc-link ez-toc-heading-4" href="https://quietbo.com/2022/07/21/golang-%e5%ae%89%e8%a3%9d-windows-ubuntu20-04/#%E5%B7%B2%E8%A7%A3%E6%B1%BA_%E9%97%9C%E6%8E%89%E7%B5%82%E7%AB%AF%E6%A9%9F%E6%89%BE%E4%B8%8D%E5%88%B0go" >[已解決] 關掉終端機找不到go</a>
        </li>
        <li class='ez-toc-page-1 ez-toc-heading-level-3'>
          <a class="ez-toc-link ez-toc-heading-5" href="https://quietbo.com/2022/07/21/golang-%e5%ae%89%e8%a3%9d-windows-ubuntu20-04/#%E5%9F%B7%E8%A1%8Cgo%E6%AA%94%E6%A1%88" >執行go檔案</a>
        </li>
      </ul>
    </li>
    
    <li class='ez-toc-page-1 ez-toc-heading-level-2'>
      <a class="ez-toc-link ez-toc-heading-6" href="https://quietbo.com/2022/07/21/golang-%e5%ae%89%e8%a3%9d-windows-ubuntu20-04/#%E6%A8%99%E6%BA%96%E5%91%BD%E4%BB%A4_%E2%80%93_run_%E8%88%87_build%E5%B7%AE%E7%95%B0" >標準命令 &#8211; run 與 build差異</a>
    </li>
  </ul></nav>
</div>

## <span class="ez-toc-section" id="Windows%E5%AE%89%E8%A3%9D"></span>Windows安裝<span class="ez-toc-section-end"></span> 

以下為安裝連結:  
[安裝Golang][1]  
[VSCode][2]

### <span class="ez-toc-section" id="%E5%9F%B7%E8%A1%8C%E7%AC%AC%E4%B8%80%E6%94%AF%E7%A8%8B%E5%BC%8Fhellogo"></span>執行第一支程式hello.go<span class="ez-toc-section-end"></span> 

下方為hello.go內的code

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">package main

import "fmt"

func main() {
    fmt.Println("Hello Golang")
}

// 1.撰寫程式 &gt; 建置(build) &gt; 執行程式
// 建置: go build 程式檔案的名稱

// 2. 執行程式: 輸入執行檔的檔名</code></pre>

打開終端機執行:

<pre class="wp-block-code"><code lang="basic" class="language-basic">$ go build hello.go</code></pre>

會產生hello.exe, 在終端機執行hello  
如果出現錯誤訊息

<pre class="wp-block-code"><code lang="bash" class="language-bash">Suggestion [3,General]: 找不到 hello 命令，但它確實存在於目前的位置。Windows PowerShell 預設並不會從目前的位置載入命令。如果您信任這個命令，請改為輸入 ".\hello"。</code></pre>

請改使用./hello

補充:  
若是package main出現紅色底線, 重新開機即可。

## <span class="ez-toc-section" id="ubuntu_%E5%AE%89%E8%A3%9D_golang_118"></span>[ubuntu] 安裝 golang 1.18<span class="ez-toc-section-end"></span> 

下載golang壓縮檔(如果要其他版本則自行把18換成其他版本號)

<pre class="wp-block-code"><code lang="bash" class="language-bash">wget https://dl.google.com/go/go1.18.linux-amd64.tar.gz</code></pre>

上面的命令安裝了 Golang v1.13，大多數用戶更喜歡更新版本的 Golang，當新版本出現時會不斷更新。 實現此目的的最佳方法是安裝 PPA。

解壓縮

<pre class="wp-block-code"><code lang="bash" class="language-bash">sudo tar -C /usr/local -xzf go1.18.linux-amd64.tar.gz</code></pre>

完成後ls /usr/local會多一個go的目錄

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ ls /usr/local
bin  etc  games  go  include  lib  man  sbin  share  src</code></pre>

使用指令vi /etc/profile進到檔案內, 在最下方添加,  
目的是在系統環境變量PATH中增加go的路徑

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ vi /etc/profile
export PATH=$PATH:/usr/local/go/bin</code></pre>

儲存並離開,使用下方指令立即生效

<pre class="wp-block-code"><code lang="bash" class="language-bash">source /etc/profile</code></pre>

輸入go version查看版本號

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ go version
go version go1.18 linux/amd64</code></pre>

### <span class="ez-toc-section" id="%E5%B7%B2%E8%A7%A3%E6%B1%BA_%E9%97%9C%E6%8E%89%E7%B5%82%E7%AB%AF%E6%A9%9F%E6%89%BE%E4%B8%8D%E5%88%B0go"></span>[已解決] 關掉終端機找不到go<span class="ez-toc-section-end"></span> 

開啟profile檔案

<pre class="wp-block-code"><code lang="bash" class="language-bash">nano $HOME/.profile</code></pre>

然後將以下行貼上到檔案中並儲存。

<pre class="wp-block-code"><code lang="bash" class="language-bash">export PATH=$PATH:/usr/local/go/binb</code></pre>

完成後，執行以下命令以完成安裝

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ source ~/.profile
$ go version</code></pre>

補充:  
加入環境變量後但仍出現找不到go, 或是關閉終端機就會出現找不到go, 重新開啟VM試試看  
[參考此處][3]

### <span class="ez-toc-section" id="%E5%9F%B7%E8%A1%8Cgo%E6%AA%94%E6%A1%88"></span>執行go檔案<span class="ez-toc-section-end"></span> 

上方安裝及環境沒問題後, 可執行一隻hello.go試試看

下方儲存名稱為main.go

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">package main

import "fmt"

func main() {
    fmt.Println("Hello, World")
    fmt.Println("哈囉！世界！")
}</code></pre>

打開終端機輸入

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ go run main.go
Hello, World
哈囉！世界！</code></pre>

[連結][4]

## <span class="ez-toc-section" id="%E6%A8%99%E6%BA%96%E5%91%BD%E4%BB%A4_%E2%80%93_run_%E8%88%87_build%E5%B7%AE%E7%95%B0"></span>標準命令 &#8211; run 與 build差異<span class="ez-toc-section-end"></span> 

<ul class="wp-block-list">
  <li>
    build
  </li>
</ul>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ go build 檔案名.go</code></pre>

如果沒有錯誤就產生執行檔於當前目錄, 例如執行main.go成功就會出現一個main.exe檔案在同樣路徑下

<ul class="wp-block-list">
  <li>
    run
  </li>
</ul>

<pre class="wp-block-code"><code lang="bash" class="language-bash">$ go run 檔案名.go</code></pre>

<ul class="wp-block-list">
  <li>
    直接執行golang code
  </li>
  <li>
    直接在命令行輸出程序執行結果，方便用戶調試，本質上也是先編譯再執行
  </li>
</ul>

可參考更多資訊:[Go 學習筆記（37）— 標準命令（go build 跨平台編譯、交叉編譯、go clean、go run、go fmt、go install、go get）][5]

 [1]: https://go.dev/
 [2]: https://code.visualstudio.com/
 [3]: https://volvootofinans.com/zh-TW/how-to-install-go-on-ubuntu-20-04-18-04.html
 [4]: https://go.dev/doc/code
 [5]: https://blog.csdn.net/wohu1104/article/details/106295007