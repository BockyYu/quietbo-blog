---
title: '[VirtualBox] 系統備份映象檔(必學)'
author: Bocky
type: post
date: 2021-08-12T10:23:32+00:00
url: /2021/08/12/virtualbox-系統備份映象檔/
categories:
  - virtualbox

---
最近公司電腦壞掉，換了一台同型號的筆電，把舊筆電的VM備份起來，到新的電腦裡面繼續使用，說真的很簡單，我用過兩個方式都成功，但方法二花費時間比較久。

## 方法一 {.wp-block-heading}

<ol class="wp-block-list">
  <li>
    找出目前存放VM的位置，複製整個資料夾<br />怕找錯的話可以去VirtualBox裡面確認路徑，一般>進階>快照資料夾。<br />我是複製ubuntu20.04這整個資料夾，<br />注意:一定要有.vbox檔案，如果沒有複製到就沒有用<br /><img decoding="async" src="https://i.imgur.com/JvV0OEZ.png" alt="" />
  </li>
  <li>
    資料夾複製到新電腦<br />點選VirtualBox的加入，找到剛複製的資料夾位置<br /><img decoding="async" src="https://i.imgur.com/NQJrfma.png" alt="" />
  </li>
  <li>
    加入.vbox檔案<br /><img decoding="async" src="https://i.imgur.com/1fn4Ko2.png" alt="" />
  </li>
  <li>
    加入成功<br /><img decoding="async" src="https://i.imgur.com/FQ1iMaD.png" alt="" />
  </li>
</ol>

這是沿用之前的VM，不算有備份(除非有做快照)，未來若VM有問題，只能用快照復原。  
(除非有把原本複製過來時的資料夾保留著)

## 方法二 {.wp-block-heading}

此方法是直接用VirtualBox的匯出功能，雖然等的時間真的很長但做出來的.ova檔案，算是備份檔了。

<ol class="wp-block-list">
  <li>
    打開VirtualBox，點選匯出<br /><img decoding="async" src="https://i.imgur.com/RvO8Rhn.png" alt="" />
  </li>
  <li>
    選擇要匯出的VM後下一步<br /><img decoding="async" src="https://i.imgur.com/by4suO7.png" alt="" />
  </li>
  <li>
    依個人狀況去選擇，我只有調整MAC原則網址<br /><img decoding="async" src="https://i.imgur.com/oMJZZRL.png" alt="" />
  </li>
  <li>
    再下一步後開始匯出(這時間真的要等很久)<br /><img decoding="async" src="https://i.imgur.com/IEcbNLI.png" alt="" />
  </li>
  <li>
    匯入ova檔<br />成功匯出後把.ova檔案複製到新電腦上，然後到新電腦匯入.ova檔<br />位置放在自己找的到的位置即可
  </li>
</ol><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/bmPlc1P.png" alt="" /> </figure> 

<ol class="wp-block-list" start="6">
  <li>
    開始匯入<br /><img decoding="async" src="https://i.imgur.com/tyFMqdI.png" alt="" />
  </li>
  <li>
    等待匯入<br /><img decoding="async" src="https://i.imgur.com/kdd2wfN.png" alt="" />
  </li>
  <li>
    匯入成功
  </li>
</ol>

匯入成功的VM已經跟ova檔無關了，可以參考方法一看VM的路徑位置在哪，未來如果這支匯入的VM掛了，就可以再拿ova重新匯入，只是這之後的軟體和檔案要重新下載。

如果想要用別人的VM，就請對方匯出ova檔，再做匯入即可。