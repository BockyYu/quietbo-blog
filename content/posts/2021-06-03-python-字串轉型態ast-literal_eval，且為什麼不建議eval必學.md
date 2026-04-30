---
title: '[Python]字串轉型態ast.literal_eval，且為什麼不建議eval(必學)'
author: Bocky
type: post
date: 2021-06-03T09:40:06+00:00
url: /2021/06/03/python-字串轉型態ast-literal_eval，且為什麼不建議eval必學/
categories:
  - Python
  - 程式語言
tags:
  - python

---
三分鐘學習一個小知識，還有範例直接看!

當python在做型態轉換，str轉dict、list、tuple、set或是int時，有些人會使用eval 或 ast.literal_eval，但eval是不推的，安全性是其中重要的原因。  
若要單純轉換型態，我。

稍微講一下eval會說是危險原因:

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers"># coding:utf-8

"""
輸入下方指令:
"1000"
"1+3"
"[0, 1, [2, 2]]"
"(1, 3, 5, [7])"
"{'A': 'aa', 'B': 'bb', 'C': 'cc'}"
"__import__('os').system('ls /')"
"""
std = input('please input: ')
eval_std = eval(std)
print('input: ',eval_std, type(eval_std))</code></pre>

以上5種輸入，下方為輸出結果:

<pre class="wp-block-code"><code lang="bash" class="language-bash">input: 1000 &lt;type 'int'&gt;
input: 4 &lt;type 'int'&gt;
input: [0, 1, [2, 2]] &lt;type 'list'&gt;
input: (1, 3, 5, [7]) &lt;type 'tuple'&gt;
input: {'A': 'aa', 'C': 'cc', 'B': 'bb'} &lt;type 'dict'&gt;

bin  boot  cdrom  dev  etc  home  lib  lib32  lib64  libx32  lost+found  media    mnt  opt  proc  root  run  sbin  snap  srv  swapfile  sys  tmp  usr  var  VBox.log
input: 0 &lt;type 'int'&gt;</code></pre>

eval 不只是可以轉型態、將輸入做處理，甚至系統的命令都能執行!  
如果今天(使用者)輸入的內容是輸入刪除文件、顯示目錄結構等命令，那是很大的危險，所以要轉型態是不建議使用eval的!(本篇不介紹惡意操作的指令有哪些)

使用下方程式:ast.literal_eval

<pre class="wp-block-code"><code lang="python" class="language-python line-numbers"># coding:utf-8
import ast

"""
輸入下方指令:
"1000"
"1+3" # 會報錯
"[0, 1, [2, 2]]"
"(1, 3, 5, [7])"
"{'A': 'aa', 'B': 'bb', 'C': 'cc'}"
"__import__('os').system('ls /')"   # 會報錯
"""
std = input('please input: ')
ast_std = ast.literal_eval(std)
print('input: %s %s'% (ast_std, type(ast_std)))</code></pre>

ast.literal_eval會去判斷要解析的內容是否安全，不安全就報錯，我們只要處理報錯的處理就好，比起找回刪除的檔案或是被偷的資料，這輕鬆多了。

結論:字符串進行類型轉換，一律用ast.literal_eval()

連結:[python document][1]

 [1]: https://docs.python.org/2/library/ast.html