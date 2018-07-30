---
title: Linux下安装samba服务
date: 2018-07-09 01:08:36
tags:
	- samba 
---
samba作用：主要用于window和linux系统之间进行共享文件。

步骤如下:

1.yum安装samba
```shell
yum install -y samba
```

2.安装好之后在建立一个用户(把同时创建用户的家作为共享文件目录)
```shell
useradd	samtest
passwd	samtest
```

3.将系统用户加入到samba配置里面
```shell 
smbpasswd -a samtest(刚刚创建的用户)
```

后面链接会提示输入密码(如123456)(window连接的密码)

4.启动samba服务,命令如下
```shell
service smb start
```

5.window连接
	快捷键win+r:输入`\\192.168.247.129`(linux的ip地址)
	后面会提示输入用户名和密码:samtest 123456

6.在window中可将共享目录映射为网络驱动器,后续可以直接去计算机中打开,操作起来更加方便。
