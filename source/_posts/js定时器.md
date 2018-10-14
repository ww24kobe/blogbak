---
title: js定时器
date: 2018-09-18 16:02:30
tags:
	- JavaScript
---

## 什么时定时器

JS提供了一些原生方法来实现`延时或定时`去执行某一段代码,如下两个函数：
- setInterval  定时器
- setTimeout   延时器

### setInterval  定时器

语法：

```javascript
var timeoutId = window.setInterval(func,milliseconds);
```

   参数：

   - func，定时要执行的函数。
   - milliseconds， 定时执行的时间（单位：毫秒 ）

   返回值：

timeoutId：所设置定时器返回的id。可以传递此值给`window.clearTimeout()`以取消定时器

   

### setTimeout延时器

语法：

```javascript
var intervalID = window.setTimeout(func,milliseconds);
```

参数：

- func，定时要执行的函数。
- milliseconds， 定时执行的时间（单位：毫秒 ）

返回值：

intervalID：所设置延时器返回的id。可以传递此值给`window.clearTimeout()`以取消延时器



## 示例

### 定时器，实现每隔5秒说我爱你

```javascript
   var intervalID = window.setInterval(function(){ 
   	console.log('i love you');
   },5000);
```

   > 一般可以把window给省略，它时全局对象。可以不写。
   >
   > 如弹窗: window.alert('123');  或 alert('123')也可以

清除定时器：

```javascript
 clearInterval(intervalID);
```



### 延时器，延时5秒说我爱你

```javascript
var timeoutID = window.setTimeout(function(){ 
	console.log('i love you');
},5000);
```

清除延时器：

```javascript
 clearTimeout(timeoutID);
```



### 注意：

- 什么时候情况下要用到延时器，什么情况下需要用到定时器？
- 只需要执行一次的我们就使用延时器 
- 无限次执行的我们就使用定时器