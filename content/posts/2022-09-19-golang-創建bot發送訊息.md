---
title: '[Golang] 創建BOT&發送訊息'
author: Bocky
type: post
date: 2022-09-19T10:00:42+00:00
url: /2022/09/19/golang-創建bot發送訊息/
categories:
  - BOT
  - golang
tags:
  - golang

---
## 創建BOT，加入好友並取得token 

打開Telegram搜尋:  
@BotFather  
<img decoding="async" src="https://i.imgur.com/cZZDRgu.png" alt="" /> 

加入好友後，輸入/start 會提供些指令讓你選擇。

<ul class="wp-block-list">
  <li>
    /start :用戶開始和機器人進行交互
  </li>
  <li>
    /help :返回幫助信息
  </li>
  <li>
    /setting :返回機器人的設置界面用戶在首次向機器人發信息之前會看到/start按鈕，在菜單中（機器人信息頁）可以看到幫助和設置鏈接。
  </li>
</ul>

創建BOT過程如下, 成功會返回一段訊息:  
<img decoding="async" src="https://i.imgur.com/2NosBTo.png" alt="" /> 

藍框: 用來加該機器人好友的，建議直接點擊加入，先成為好友。  
紅框: 該bot的token，主要用來操控BOT，要記住!!

## 取得chat id 

需要chat id，bot才知道要傳送訊息給哪個使用者或群組。

首先，加入Bot好友後，傳一個訊息給這支BOT，例如&#8221;testbot&#8221;，發送成功後打開瀏覽器輸入

<pre class="wp-block-code"><code class="">https://api.telegram.org/bot{token}/getUpdates</code></pre>

範例:  
https://api.telegram.org/bot5630000628:AAH2XXXXXXXXXXXXXXXXXXXXXXXXXXXXn2zo/getUpdates

會看到json資料，從裡面我們可以得到chat_id，建議先利用這網站把Json轉成可讀性高一點  
[JSON格式化][1]  
轉成功後再貼在記事本，搜尋剛剛傳給bot的訊息:testbot  
會看到有一段，像下圖的訊息<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/NwJIyNx.png" alt="" /> </figure> 

取得那段數字就好。

## 使用程式發送訊息 

把chat id和token帶入下方的const內。

並開啟終端機輸入:go get -u github.com/go-telegram-bot-api/telegram-bot-api

<pre class="wp-block-code"><code lang="go" class="language-go line-numbers">package main

import (
    "fmt"
    tgbotapi "github.com/go-telegram-bot-api/telegram-bot-api"
    "log"
)
var bot *tgbotapi.BotAPI

const (
    chatID   = 1234567    //要傳送訊息給指定用戶
    youToken = "5630000628:AAH2XXXXXXXXXXXXXXXXXXXXXXXXXXXXn2zo"
)

func main() {
    var err error
    bot, err = tgbotapi.NewBotAPI(youToken)
    if err != nil {
        log.Fatal(err)
    }
    bot.Debug = false

    link := fmt.Sprintf(`&lt;a href="%s"&gt;[google]&lt;/a&gt;`, "https://www.google.com.tw/")
    sendMsg(link)
}

func sendMsg(msg string) {
    NewMsg := tgbotapi.NewMessage(chatID, msg)
    NewMsg.ParseMode = tgbotapi.ModeHTML   //傳送html格式的訊息
    _, err := bot.Send(NewMsg)
    if err == nil {
        log.Printf("Send telegram message success")
    } else {
        log.Printf("Send telegram message error")
    }
}</code></pre>

使用程式運行發送後就會收到 google 連結的的訊息了  
<img decoding="async" src="https://i.imgur.com/auvOu34.png" alt="" />

 [1]: https://tw.piliapp.com/json/formatter