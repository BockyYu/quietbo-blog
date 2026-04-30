---
title: '[MySQL] MySQL InternalError: 1251, u’Client does not support authentication protocol requested by server; consider upgrading MySQL client'
author: Bocky
type: post
date: 2021-05-11T11:13:00+00:00
url: /2021/05/11/解決-internalerror-1251-uclient-does-not-support-authentication-protocol-requested-by-server-consider-upgrading-mysql-client/
categories:
  - MySQL
tags:
  - Mysql

---
某次在local測試時，因為要新增package而重新build了一次docker。  
後來更新get-pip出現錯誤訊息如下:

<pre class="wp-block-code"><code lang="bash" class="language-bash">InternalError: (1251, u'Client does not support authentication protocol requested by server; consider upgrading MySQL client')</code></pre>

  
客戶端不支持服務器請求的身份驗證協議；請考慮升級MySQL客戶端

目前是使用python2.7，MySQL 8.0.23，  
不推薦將MYSQL降級，可以通過在創建數據庫時告訴MySQL服務器使用舊版身份驗證插件來實現此目的。

<pre class="wp-block-code"><code lang="sql" class="language-sql">ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
flush privileges;</code></pre><figure class="wp-block-image">

<img decoding="async" src="https://i.imgur.com/5j9Eex7.png" alt="" /> </figure> 

如果不行的話，將@&#8217;localhost&#8217;拿掉，再重新執行一次，下方還有其他指令，可嘗試以下指令擇一試看看。

<pre class="wp-block-code"><code class="">ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '123456';
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123456';
ALTER USER 'root'@'localhost' IDENTIFIED BY '123456' PASSWORD EXPIRE NEVER;
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123456';
FLUSH PRIVILEGES; # 最後一定要加這段</code></pre>

我是將@&#8217;localhost&#8217;拿掉後，才成功的。若失敗的話，請參考下方連結，內有許多解決方式。  
參考連結:<a rel="noreferrer noopener" href="https://stackoverflow.com/questions/50093144/mysql-8-0-client-does-not-support-authentication-protocol-requested-by-server/50961428" target="_blank">stackoverflow</a>、<a rel="noreferrer noopener" href="https://blog.csdn.net/lovedingd/article/details/106728292" data-type="URL" data-id="https://blog.csdn.net/lovedingd/article/details/106728292" target="_blank">Mysql 解決1251</a>