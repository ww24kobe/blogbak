---
title: js之eval函数
date: 2018-07-09 01:13:36
tags:
	- javascript
---



语法：
```javascript
eval(参数)
```

作用：会把eval函数中的参数当成js代码来执行。

一般在js中解析响应的json数据的时候都是使用`JSON.parse()`来实现，但是也可以使用eval函数将json字符串变为js可以解析的变量。
如下：
```javascript
eval("var json =" + json字符串)
```

但是强烈不建议使用，因为此方法非常`危险`！！ 因为会覆盖当前作用域的同名变量。

```javascript
function test(){
    var a = 100;
   //把一个字符串变为js代码执行，此字符串也可能是接口返回的。
    eval("var a = 200;");
    console.log(a); // 200 覆盖了 局部变量a
}
test();
```
如果改为严格模式，就不会覆盖，就是100。如下：
```js
function test(){
    'use strict';
    var a = 100;
   //把一个字符串变为js代码执行，此字符串也可能是接口返回的。
    eval("var a = 200;");
    console.log(a); // 100 
}
test();
```

如果真想使用eval函数进行一些处理，建议使用new Function的形式进行替代处理，因为函数内的变量是局部变量的,就不会影响函数外部的同名变量。
如下：

```javascript
function test(){
    var a = 100;
    var fn = new Function('',"var a = 200; return a;");
    console.log(a);  // 100
    return fn();  
}
console.log( test() ); // 200
```

>所以，对于学习eval的建议是，认识而不使用


