---
title: '[Python] ‘cryptography’ package is required for sha256_password or caching_sha2_password auth methods'
author: Bocky
type: post
date: 2022-03-30T02:56:35+00:00
url: /2022/03/30/python-cryptography-package-is-required-for-sha256_password-or-caching_sha2_password-auth-methods/
categories:
  - Python

---
環境:

<pre class="wp-block-code"><code lang="bash" class="language-bash">windows10
mysql  Ver 8.0.28
python3.7, mysql+pymysql</code></pre>

開發時要連線到MySQL時出錯，錯誤訊息如下:  
<img decoding="async" src="https://i.imgur.com/Xr9yP8Z.png" alt="" /> 

<pre class="wp-block-code"><code lang="bash" class="language-bash">cryptography' package is required for sha256_password or caching_sha2_password auth methods"
RuntimeError: 'cryptography' package is required for sha256_password or caching_sha2_password auth methods</code></pre>

去google才得知:  
MySQL 自8.0+ 版本後，默認的身份認證插件由mysql\_native\_password 變為了caching\_sha2\_password,  
網上提供的作法，有些答案都是去MySQL中更改默認的認證方式，但我不建議這麼做，原因就是未來部屬時，問題仍有可能會再次出現。

解決方式:

<pre class="wp-block-code"><code lang="bash" class="language-bash line-numbers">pip3 install cryptography</code></pre>

密碼學:  
什麼是cryptography?可[參考連結][1]

 [1]: https://cryptography.io/en/latest/