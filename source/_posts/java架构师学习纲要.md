---
title: java架构师学习纲要
date: 2019-03-01 11:50:42
tags: java 
categories: java
---
# java架构师相关学习

19年上半年学习计划
 
 * java架构师相关学习

 * 大数据应用相关实战
 
 * java数据结构与算法

 大数据: 公有云,大数据
 java, 云计算, 大数据

 unix文件系统
 目录     概述
/           /也被称为"斜杠"或者根
/bin        由系统,系统管理源以及用户共享的通用程序
/boot       Boot文件,启动加载器(grup),内核,vmlinuz
/dev        包含了对系统设备,带有特殊属性的文件的引用
/etc 	    重要的系统文件配置
/home	    系统用户的主目录
/lib        库文件,包括系统和用户都需要的所有类型的
/lost+found 文件操作失败会被保存在这里
/mnt        外部文件系统的标准挂载点.
/media      外部文件系统(或者某些发行版)的挂载点
/net        整个远程文件系统的标准挂载点-nfs
/opt        一般都是包含一些附加的或者第三方软件
/proc		一个包含了系统资源相关信息的虚拟文件系统
/root		root用户的主目录.
/sbin 		由系统和系统管理员来使用的程序
/tmp        供系统使用的临时空间,重启时会被清空.
/usr		供所有用户相关程序使用的程序,库,文档等等
/var 		存储所有用户创建的可变文件和临时文件.比如日志文件,邮件队列,后台打印程序,WEB服务器,数据库等等.
/etc/passwd 包含了本地linux的用户.
/etc/shadow 包含了哈希过的本地账户密码.
/etc/group	包含了本地账户分组
/etc/init.d/ 包含了初始化脚本-具体都安装了些啥应该值得一瞧.
/etc/hostname  系统的hostname.
/etc/network/interface 网络接口
/etc/resolv.conf  	系统的DNS服务
/etc/profile  系统的环境变量
~/.ssh/	 	 SSH密钥
~/.bash_history 	用户的bash历史日志
/var/log/ 	 Linux系统的日志文件一般就存放在这里
/var/adm/ 	 UNIX系统的日志文件一般就存放在这里
/var/log/apache2/access.log  Apache访问日志文件通常的存在路径
/var/log/httpd/accss.log
/etc/fstab    挂载的文件系统

查找
find -name tecmint.txt
find /home -name tecmint.txt
find /home -inname tecmint.txt
find / -type d -name Tecmint
find . -type f -name tecmint.php
find . -type f -name "*.php"


