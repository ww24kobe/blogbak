---
title: centOs中php5.6安装memcache扩展
date: 2018-08-05 13:01:09
tags:
	- memcache
	- centos
	- nosql
---

环境：centos、php5.6、memcache2.2.7



- 步骤1：先下载php的memcache扩展

  ```shell
  wget http://pecl.php.net/get/memcache-2.2.7.tgz
  ```

- 步骤2：tar解压,进入解压后的目录

  ```shell
  tar zxf memcache-2.2.7.tgz
  cd memcache-2.2.7
  ```

- 步骤3：找到php的phpize的扩展工具，生成configure文件

  ```shell
  /usr/local/php/bin/phpize
  ```

- 步骤4：执行./configure,收集系统安装环境的信息

  ```shell
  ./configure  --with-php-config=/usr/local/php/bin/php-config
  ```

- 步骤5：编译和安装

  ```shell
  make && make install
  ```

  成功之后会在目录 `/usr/local/php/lib/php/extensions/no-debug-non-zts-20131226/`生成`memcache.so`的动态库文件。


- 步骤6：修改php的php.ini配置文件加上memcache.so扩展

  ```shell
	extension=/usr/local/php/lib/php/extensions/no-debug-non-zts-20131226/memcache.so 
  ```
通过`php -m |grep memcache`查看含有memcache模块说明安装成功




