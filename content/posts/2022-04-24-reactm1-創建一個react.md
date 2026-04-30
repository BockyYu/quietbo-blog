---
title: '[React|M1] 創建一個React'
author: Bocky
type: post
date: 2022-04-24T14:21:02+00:00
url: /2022/04/24/reactm1-創建一個react/
categories:
  - React
tags:
  - React

---
Mac M1

參考[github:create-react-app][1]

點擊網站來安裝[Node.js][2]  
<img decoding="async" src="https://i.imgur.com/5YcVEgv.png" alt="" /> 

查看是否安裝成功

<pre class="wp-block-code"><code class="">node -v
npm -v</code></pre>

創建一個react

<pre class="wp-block-code"><code class="">npx create-react-app react-store</code></pre>

打開剛才創建的react

<pre class="wp-block-code"><code class="">cd react-store
npm start</code></pre>

成功如下:

<pre class="wp-block-code"><code class="">  Local:            http://localhost:3000
  On Your Network:  http://192.168.100.4:3000

Note that the development build is not optimized.
To create a production build, use npm run build.

webpack compiled successfully</code></pre>

打開瀏覽器填入http://localhost:3000/  
<img decoding="async" src="https://i.imgur.com/gIAkRbN.png" alt="" />

 [1]: https://github.com/facebook/create-react-app
 [2]: https://nodejs.org/en/