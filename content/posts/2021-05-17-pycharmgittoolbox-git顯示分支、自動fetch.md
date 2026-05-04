---
title: '[Pycharm]GitToolBox – Git顯示分支、自動Fetch'
author: Bocky
type: post
date: 2021-05-17T14:12:47+00:00
url: /2021/05/17/pycharmgittoolbox-git顯示分支、自動fetch/
categories:
  - Editor;IDE;GUI

---
GitToolBox 是IDE插件，我個人是滿推薦安裝的，下方有一些截圖和功能說明，如果這是你想要的工具，你想安裝的話，可以參考下方的安裝、設定方式。

## 顯示git Branch、Fetch和最後commit的時間和訊息 

<img decoding="async" src="https://i.imgur.com/Lz0pHKL.png" alt="" />  
Δ-表示有變化  
∅-不變/乾淨

舉例:  
2Δ-表示有2個變化(Fetch)。

Fetch會自動檢查，若不想要太常檢查可以自行設定。

下圖是我隨便截的一段程式碼，在26行是我光標停放的位置，會顯示該行git最後commit的時間和訊息，這也是能夠自己設定格式。  
<img decoding="async" src="https://i.imgur.com/61gLzih.png" alt="" /> 

## 安裝、使用方式 

本次操作版本為:11.0.6  
安裝方法:  
File -> Settings -> Plugins -> GitToolBox -> Installed  
<img decoding="async" src="https://i.imgur.com/ZIxUJmc.png" alt="" />  
安裝過程或許會較久，若安裝完成建議重開Pycharm。

使用方法:  
File -> Settings -> Other Settings -> GitToolBox Global 或 GitToolBox Project  
<img decoding="async" src="https://i.imgur.com/jrMK0sC.png" alt="" />  
這兩個都可以進去修改。

[點選我獲得更詳細的操作][1]

 [1]: https://github.com/zielu/GitToolBox/wiki/Manual#git-status-display