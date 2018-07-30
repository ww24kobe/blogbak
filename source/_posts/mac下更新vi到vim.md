---
title: mac下更新vi到vim
date: 2018-07-30 12:09:07
tags:
	- vim
	- mac
---

mac自带vim，但是并不是最新版本，如果我们需要更新vim。 
1.安装homebrew，如果已安装则不需要安装，

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"1
```

2.安装Vim

```
brew install vim
```

3.检测是否成功

```
vim --version
```