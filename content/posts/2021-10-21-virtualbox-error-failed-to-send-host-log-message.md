---
title: '[VirtualBox] ERROR Failed to send host log message'
author: Bocky
type: post
date: 2021-10-21T10:20:13+00:00
url: /2021/10/21/virtualbox-error-failed-to-send-host-log-message/
categories:
  - virtualbox

---
某次要重開ubuntu時出現的錯誤訊息:

<pre class="wp-block-code"><code class="">[drm:vmw_host_log [vmwgfx]] ERROR Failed to send host log message</code></pre>

  
<img decoding="async" src="https://i.imgur.com/S2fjQh6.png" alt="" /> 

解決方式:  
設定 -> 顯示 -> 畫面 -> 圖形控制器 -> VBoxVGA  
<img decoding="async" src="https://i.imgur.com/HjhGz0L.png" alt="" />