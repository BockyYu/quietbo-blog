---
title: '[Python 3.6] f-Strings (字串雙引號前加f)'
author: Bocky
type: post
date: 2022-02-21T07:03:38+00:00
url: /2022/02/21/python-3-6-f-strings-字串雙引號前加f/
categories:
  - Python
tags:
  - python

---
Python 3.6之前式字串格式化:

<pre class="wp-block-code"><code class="">str.format()</code></pre>

處理多個引數和更長的字串時，程式碼很冗長

f-Strings 比 %-formatting 和 str.format()更輕鬆，且更快。  
大小寫f都可以使用:

<pre class="wp-block-code"><code lang="basic" class="language-basic">&gt;&gt;&gt; name = "Bocky"
&gt;&gt;&gt; age = 18
&gt;&gt;&gt; f"name={name}, age={age}"
'name=Bocky, age=18'</code></pre>

也可以運算:

<pre class="wp-block-code"><code lang="bash" class="language-bash">&gt;&gt;&gt; f"{2*100}"
'200'</code></pre>

使用function:

<pre class="wp-block-code"><code lang="bash" class="language-bash">&gt;&gt;&gt; def to_lowercase(input):
...     return input.lower()
...
&gt;&gt;&gt; name = "BOCKY"
&gt;&gt;&gt; f"{to_lowercase(name)} is funny."
'bocky is funny.'</code></pre>

[文檔:2.4.3. Formatted string literals][1]

[參考2][2]

 [1]: https://docs.python.org/3/reference/lexical_analysis.html#f-strings
 [2]: https://iter01.com/585538.html