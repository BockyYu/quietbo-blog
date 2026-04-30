---
title: '[VirtualBox] 無法開啟虛擬機 Not in a hypervisor partition (HVP=0)'
author: Bocky
type: post
date: 2021-08-12T09:09:32+00:00
url: /2021/08/12/virtualbox-無法開啟虛擬機-not-in-a-hypervisor-partition-hvp0/
categories:
  - virtualbox

---
最近公司電腦壞掉，換了一台同型號的筆電，把舊筆電的VM備份起來，到新的電腦裡面繼續使用，結果才剛開始就出現問題:

  
Not in a hypervisor partition (HVP=0) (VERR\_NEM\_NOT\_AVAILBLE). VT-x is disabled in the BIOS for all CPU modes (VERR\_VMX\_MSR\_ALL\_VMX\_DISABLED)<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/p9sTP6W.png" alt="" /> </figure> 

解決方式:  
1.重新開機進入BIOS，每個廠牌的筆電，進BIOS的按鍵都不一樣，請自行查詢。  
2.找到Intel(R) Virtualization Technology  
3.Enabled (啟用)  
4.存檔後離開  
5.打開VirtualBox