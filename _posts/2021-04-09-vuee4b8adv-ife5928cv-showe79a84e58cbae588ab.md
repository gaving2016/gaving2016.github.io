---
id: 134
title: Vue中v-if和v-show的区别
date: '2021-04-09T09:21:56+08:00'
author: gavin
layout: post
guid: 'https://gaving.top/?p=134'
permalink: /index.php/2021/04/09/vue%e4%b8%adv-if%e5%92%8cv-show%e7%9a%84%e5%8c%ba%e5%88%ab/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Vue
---

<div class="blog-content-box"><article class="baidu_pl"><div class="article_content clearfix" id="article_content"><div class="markdown_views prism-atom-one-dark" id="content_views">`v-if`控制 DOM的删除和添加，不同于`v-show`对DOM的显示和隐藏

</div><div><div>v-show严格意义上说“**条件隐藏**”。浏览器首先不管三七二十一，把**HTML元素先渲染起来，符合条件就显示，不符合条件display就为none，不显示，但是元素还在那。**</div><div>v-if是真正意义上的“**条件渲染**”。浏览器先判断符不符合条件，**符合了再渲染，否则不渲染DOM，浏览器中找不到这个DOM**。

</div>v-if由于是重新渲染，所以每次切换一次会重新走一次生命周期，v-show由于只是控制显示隐藏，所以除了初始化渲染，其他时候都不会再走相关生命周期了。

性能差别：

</div>1、v-if有更高的切换开销，v-show有更高的初始渲染开销。如果需要频繁的切换，使用v-show比较好，如果运行条件很少改变，使用v-if比较好。

2、v-show比v-if性能更高，因为v-show只能动态的改变样式，不需要增删DOM元素。所以当程序不是很大时候，v-if和v-show区别都不大，如果项目很大，推荐多用v-show，较少浏览器后期操作的性能。

3、需要多种条件场景，比如id=1，=2，=3.....时候，因为只有v-if，可以和v-else等连用，这种比较适合用v-if

4、v-show不支持<template>语法

5、v-if切换时候回实时的销毁和重建内部的事件、钩子函数等，v-show只会初始化渲染时候执行，再切换时候不会执行生命后期的过程。

</div></article></div><script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>