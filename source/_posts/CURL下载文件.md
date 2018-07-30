---
title: CURL下载文件
date: 2018-07-09 01:11:01
tags:
	- php 
---

首先需要在php.ini配置文件中开启`extension=php_curl.dll`模块。

方法如下：
```php
function curl_download_file($url,$save_to)
{
    $ch=curl_init();
    curl_setopt($ch,CURLOPT_POST,0);
    curl_setopt($ch,CURLOPT_URL,$url);
    curl_setopt($ch,CURLOPT_RETURNTRANSFER,1);
    $file_content=curl_exec($ch);
    //方式一：
    file_put_contents($save_to, $file_content);
    //方式二：
    /*$downloaded_file=fopen($save_to,'w');
    fwrite($downloaded_file,$file_content);
    fclose($downloaded_file);*/
}

```
测试：
```php
$url="http://f.hiphotos.baidu.com/image/h%3D300/sign=469a7dc8dd58ccbf04bcb33a29d8bcd4/aa18972bd40735fa13899ac392510fb30f24084b.jpg";
curl_download_file($url,time().'.jpg'); //这里需获取url的后缀
```
