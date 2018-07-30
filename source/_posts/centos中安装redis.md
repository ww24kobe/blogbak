---
title: centos中安装redis
date: 2018-07-09 00:50:46
tags:
	- nosql
	- redis
---
## 1.下载redis

下载地址：http://download.redis.io/releases/
![image.png](https://upload-images.jianshu.io/upload_images/11273713-e9d71c4023c90288.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
使用wget命令下载到自己的目录中：
```shell
wget http://download.redis.io/releases/redis-4.0.10.tar.gz
```
这里我是下载4版本，你可以选个版本进行安装
## 2.安装redis
进入到下载的redis所在目录,依次执行以下命令
```shell
tar -zxf redis-4.0.10.tar.gz 
cd redis-4.0.10
make && make install
```
复制配置文件redis-conf到/etc/目录下，方便管理。
```shell
cp redis.conf /etc/
```

安装好后查看redis的服务端和客户端的编译后文件位置
```
 find /usr/local/ -name redis-*
```
结果：
```
/usr/local/bin/redis-server
/usr/local/bin/redis-cli
/usr/local/bin/redis-check-aof
/usr/local/bin/redis-check-rdb
/usr/local/bin/redis-sentinel
/usr/local/bin/redis-benchmark
```
或者通过which查看指令的所在路径：
```
which redis-cli redis-server
```
> 没有通过 make  install 指定安装目录一般默认安装在/usr/local/bin下面，若指定安装目录可以使用: `make PREFIX=/usr/local/redis  install`

## 3.启动redis服务
打开redis.conf配置文件，设置为redis服务在后台运行。
```
vim /etc/redis.conf 
```
把no改为yes 
![image.png](https://upload-images.jianshu.io/upload_images/11273713-11a8518b13952bb1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

启动服务
```shell
/usr/local/bin/redis-server  /etc/redis.conf
```

确认是否启动成功
``` shel
ps -aux |grep redis-server
```
若要杀死服务执行`pkill -9 redis`即可
## 4、连接redis
语法
```shell
redis-cli -h ip 地址 -p 端口号 -a 密码
```
> 如果是本地连接默认ip为127.0.0.1，端口默认为6379，默认没密码，但通过redis,conf可以设置，没改配置直接通过redis-cli命令连接即可。
- 若要开启密码,找到配置文件redis.conf的requirepass处,去掉前面的注释#，设置密码
- 如要修改默认端口，找到配置文件redis.conf的port 6379处，设置其他端口号即可，修改之后保存退出，需杀死redis服务，重新开启服务

连接redis

```shell
/usr/local/bin/redis-cli -h 127.0.0.1 -p 6379
```
进入到redis命令的交互窗口，进行测试：
![image.png](https://upload-images.jianshu.io/upload_images/11273713-e1244fd46f4a3576.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

至此，redis安装成功。
