---
id: 155
title: ThinkPHP5框架where实现or查询
date: '2021-05-06T00:31:13+08:00'
author: gavin
layout: post
guid: 'https://gaving.top/?p=155'
permalink: /index.php/2021/05/06/thinkphp5%e6%a1%86%e6%9e%b6where%e5%ae%9e%e7%8e%b0or%e6%9f%a5%e8%af%a2/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - PHP
---

1.采用闭包方式  
tp5中采用闭包的方式：  
$map\['user\_id'\]=1;  
$map\['status'\]=0;  
$or\_map\['user\_id'\]=$map\['user\_id'\];  
$or\_map\['audit'\]=\['in',\['1,2'\]\];  
$list = Db::name('table')->where(function ($query) use ($map) {  
$query->where($map);  
})-><span style="color: #ff0000;">whereOr</span>(function ($query) use ($or\_map) {  
$query->where($or\_map);  
})->select();  
//生成的sql语句：  
//SELECT \* FROM `tp\_table` WHERE ( `user\_id` = '1' AND `status` = 0 ) OR ( `user\_id` = '1' AND `audit` IN ('1,2') )

2.普通方式

$where = \[  
'feed\_uid' => \[ 'eq' , 5\] ,  
'status' => \[ \[ 'eq' , 1\] , \[ 'eq' , 2 \] , \[ 'eq' , 3 \] , '<span style="color: #ff0000;">or</span>' \] ,  
\];  
$value = DealSpace::where($where)->count();  
//最终的查询条件为where feed\_uid=5 and (status=1 or status =2 or status =3 )

<div id="gtx-trans" style="position: absolute; left: 316px; top: 468px;"><div class="gtx-trans-icon"></div></div><script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>