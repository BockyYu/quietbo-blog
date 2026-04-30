---
title: 設定windows shadowsocks與virtualbox(ubuntu)共享IP
author: Bocky
type: post
date: 2021-06-30T13:53:44+00:00
url: /2021/06/30/設定windows-shadowsocks與virtualboxubuntu共享ip/
categories:
  - 系統相關

---
最近WFH後，都要用penVPN和shadowsocks的IP來開發和測試。  
但其實我一直有一個問題沒有解決，  
就是windows開shadowsocks，但virtualbox的ubuntu20.04沒有共享到，  
最近測試又要用shadowsocks的IP，終於在今天把這問題解決了。(感謝我家技術長提供的方法)

主機系統：Windows10  
VPN：shadowsocks 4.1.9.2  
VM: virtualbox 6.1.0  
Client:ubuntu20.04

注:這裡不教設定方式，請自行上網設定完成及確認正確ip

<ol class="wp-block-list">
  <li>
    啟用windows的shadowsocks<br />shadowsocks右鍵 -> 系統代理 -> 全局模式<br /><img decoding="async" src="https://i.imgur.com/3ngWvhP.png" alt="" />
  </li>
  <li>
    顯示ubumtu路由的設定<br />在ubuntu打開終端機，執行:
  </li>
</ol>

<pre class="wp-block-code"><code lang="bash" class="language-bash">ip route show</code></pre>

我們要的是紅框內的IP(每台可能不一樣，不要抄我的IP)  
<img decoding="async" src="https://i.imgur.com/F1UQmfu.png" alt="" /> 

<ol class="wp-block-list" start="3">
  <li>
    設置Virtualbox 使用 NAT 網絡<br />之前我一直設定成橋接模式<br />設定 -> 網路 -> 附加到:NAT<br /><img decoding="async" src="https://i.imgur.com/G4Xgwb8.png" alt="" />
  </li>
</ol>

這邊設定完我會重開一次ubuntu。

<ol class="wp-block-list" start="4">
  <li>
    設置ubuntu網絡代理伺服器
  </li>
</ol>

打開ubuntu設定，  
網路 -> 網路代理伺服器 -> 手動 -> 填入在第二步驟時的ip<figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/ZYge3iA.png" alt="" /> </figure> <figure class="wp-block-image"><img decoding="async" src="https://i.imgur.com/lnwpSOT.png" alt="" /></figure> 

設定完後，網路代理伺服器會變成:手動  
<img decoding="async" src="https://i.imgur.com/ziZGQRy.png" alt="" /> 

在ubuntu開啟測試IP網址:https://www.whatismyip.com.tw  
注意:此時windows的shadowsocks是開著，ubuntu有網路連線，代理伺服器是手動。

如果IP是原本shadowsocks-windows的IP就成功了。  
<img decoding="async" src="https://i.imgur.com/NoQWLvk.png" alt="" /> 

如果開發結束，想用回原本的IP，只要把網路代理伺服器會變成:關閉  
就不會用shadowsocks-windows的IP了。

來自:[stackoverflow的文章][1]

 [1]: https://stackoverflow.com/questions/49941543/how-to-set-virtualbox-centos-7-client-to-share-host-vpn