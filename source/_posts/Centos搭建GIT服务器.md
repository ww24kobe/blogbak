---
title: Centos搭建GIT服务器
date: 2018-07-09 01:07:43
tags:
	- git 
	- Centos
---

环境：**Centos7**

## 一、 服务端安装git
第1步：先安装git工具
```shell
 yum  -y install  git
```
输入git命令测试，若出现相应的提示说明安装成功。

第2步：新建一个用户起名git
```shell 
adduser git
```

第3步：在/home/git/目录下创建一个名为.ssh的文件夹，在其.ssh目录中新建一个文件名为authorized_keys,用于保存后面生成的公钥,用于免密码提交。
```shell
cd /home/git
mkdir .ssh
touch authorized_keys
```

第4步：在git用户目录创建一个仓库（这里的仓库位置可以随意），名为project.git,在初始化此仓库
```shell
cd /home/git
mkdir project.git
git init --bare project.git
```

第5步：将git用户目录中的仓库和ssh目录的所有者和所属组都设置为git
```shell
cd /home/git
chown -R git.git project.git/
chown -R git.git .ssh/
```

第6步：修改sshd_config文件，打开RSA认证
```shell 
vim /etc/ssh/sshd_config 
``` 
开启三项：
```shell
 RSAAuthentication yes     
 PubkeyAuthentication yes     
 AuthorizedKeysFile  .ssh/authorized_keys
```

> 为了安全，禁止git用户进行shell登录，只能正常通过ssh使用git

```shell
vi /etc/passwd
注释 ##git:x:1000:1000::/home/git:/bin/bash 
改为 git:x:1000:1000:git version control:/home/git:/usr/bin/git-shell
```

至此git服务端安装完成。
现在来测试是否安装成功，这里以window系统测试为例

## 二、客户端测试-克隆git仓库
需要在客户端安装git工具，linux系统默认有不需要安装，window系统需要
下载地址：https://git-scm.com/download/win 

第1步：生成私钥和公钥，在window系统cmd命令行中输入命令 ssh-keygen  , 一路回车即可，会在当前用户的.ssh目录中生成以下两个文件：
- id_rsa 私钥
- id_rsa.pub 公钥 

需要将公钥文件内容（id_rsa.pub）提交给git服务器的管理员，他会将此公钥内容添加到服务器的`.ssh/authorized_key`文件中，一行一个。

第2步：克隆git仓库，到本地目录测试
```shell
git clone git@xxx.xxx.xxx.xxx:/home/git/project.git  ./
git add .
git commit -m 'first commit'
git push origin master
```
其中xxx.xxx.xxx.xxx为git服务器的ip地址
> 注：若提示需要密码，则检查上面的公钥和私钥是否配置成功




