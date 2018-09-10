---
title: Linux定时更新github代码脚本
date: 2018-08-08 19:47:18
tags:
	- crontab
	- git
	- Linux
---



通过`hexo+github pages`搭建的博客,每天写完后都要发布github上，为了让此项目可以在自己另外一台web服务器上访问，则每次写完后需要执行git pull origin master进行拉取代码。 为了省去这蛋疼的过程，自己在服务器写了一个小脚本，定时同步github项目到服务器web目录。


脚本sync_githubio.sh内容：
```
#!/bin/bash
cd $1
git pull origin $2
[root@wwlinux ~]#
```
 
如每30分钟执行一遍，执行命令`crontab -e`，

```
30 * * * * /root/crontab_script/sync_githubio.sh /usr/share/nginx/html/blog/ master
```


$1为执行脚本的传入的第一个参数，就是上面的 `/usr/share/nginx/html/blog/`
$2为第二个参数，`master`
$n,....以此类推，其中$0是脚本的名称（包含路径）

给脚本async_githubio.sh执行权限
```
chmod u+x sync_githubio.sh

```

就这样，是不是很简单。
