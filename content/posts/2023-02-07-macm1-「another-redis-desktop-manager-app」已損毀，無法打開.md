---
title: '[Mac|M1] 「Another Redis Desktop Manager.app」已損毀，無法打開'
author: Bocky
type: post
date: 2023-02-07T07:33:38+00:00
url: /2023/02/07/macm1-「another-redis-desktop-manager-app」已損毀，無法打開/
categories:
  - 工具類

---
執行下方指令安裝Another Redis Desktop

<pre class="wp-block-code"><code class=" line-numbers">brew install --cask another-redis-desktop-manager</code></pre>

打開Another Redis Desktop.app後會出現APP已損毀，無法打開的訊息，  
解決方式：

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">sudo spctl --master-disable
sudo xattr -rd com.apple.quarantine /Applications/Another\ Redis\ Desktop\ Manager.app
sudo spctl --master-enable
spctl --status.</code></pre>

<pre class="wp-block-code"><code class="">assessments enabled</code></pre>

重新打開APP後即成功

來源:[m1打不开，提示 “Another Redis Desktop Manager.app”已损坏，无法打开 #782][1]

 [1]: https://github.com/qishibo/AnotherRedisDesktopManager/issues/782