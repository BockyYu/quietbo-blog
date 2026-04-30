---
title: '[Pycharm] 突然連不到sql檔，檔案變成資料夾灰色叉叉 (已解決)'
author: Bocky
type: post
date: 2021-05-26T13:40:54+00:00
url: /2021/05/26/解決-pycharm-突然連不到sql檔，檔案變成資料夾灰色叉叉/
categories:
  - Editor;IDE;GUI

---
我是用網路磁碟連到ubuntu裡面的專案，就在某次要查SQL時，一直找不到檔案內的資料，後來我去看檔案，顯示如下:  
<img decoding="async" src="https://i.imgur.com/9mdbo7h.png" alt="" /> 

原本是長這樣:  
<img decoding="async" src="https://i.imgur.com/v2W2dK3.png" alt="" /> 

我是用windows查看ubuntu內的檔案，看到SQL檔變成一個資料夾左下打灰色叉，後來我試過了ubuntu重開機，windows也重開機，pycharm也用過invalid cache and restart了，仍沒有解決這問題，網路上找到的解決方式，大多都跟雲端有關，但我確定我這問題與雲端無關。  
其中也試過了刪除的方式重建，也出現不給刪除的問題。

以下是我當時解決問題的方式:

1.修改變成資料夾灰色叉的檔名 -> 成功  
2.打開已經改成新名字的檔案 -> 成功  
3.先備份一個到其他位置，取同樣的檔名後再回來把有問題的檔案刪除  
4.將檔案放回資料夾位置  
5.pycharm顯示正常了，但變成一個有修改過的格式  
6.檔案右鍵，Git -> Rollback。  
<img decoding="async" src="https://i.imgur.com/EftPDxk.png" alt="" /> 

就成功解決這問題了。  
目前有7這專案資料夾一起開，但就唯獨一個專案的SQL檔發生這問題，目前還不知道是什麼原因造成的。