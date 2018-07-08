---
title: JavaScript字符串常用方法
date: 2018-07-06 06:48:54
catgories: javascript
tags: 
	- JavaScript
	- String
---



## 字符串

- 字符串就是一个或多个排列在一起的字符，放在单引号或双引号之中。

  ```javascript
  'abc'
  "abc"
  ```

- `length`属性
  js里的字符串类似于数组，都是一个一个字符拼凑在一起组成的，因此可以用`length`属性取得字符串的长度

  ```javascript
  var str = "hello"
  str.length;  // 5
  ```

## 字符串常用的一些方法

### 1. charAt()

```javascript
str.charAt(n)
```

作用： 返回字符串的第 n 个字符，如果不在 0~str.length-1之间，则返回一个空字符串。

```javascript
var str = "javascript";
console.log( str.charAt(5) ); // 'c'
console.log( str.charAt(15) ); // ''
```

### 2. indexOf()

```javascript
indexOf(substr[,start])
```

作用： 返回 substr 在字符串 str 中首次出现的位置,从 start 位置开始查找，如果不存在，则返回 -1。 
start可以是任意整数，默认值为 0。 

```javascript
var str = "javascript";
console.log( str.indexOf('s') );   // 4
console.log( str.indexOf('php',5) ); // -1
console.log( str.indexOf('a',2) );  // 3
```

### 3. lastIndexOf()

```javascript
lastIndexOf(substr[,start])
```

作用： 返回 substr 在字符串 str 中最后出现的位置,从 start 位置 向前开始查找，如果不存在，则返回 -1。

```javascript
console.log( 'javascript'.lastIndexOf('a') ); // 3
console.log( 'javascript'.lastIndexOf('o') ); // -1
```

### 4. substring()

```javascript
str.substring(start[, end])
```

作用：返回从 start 到 end（不包括）之间的字符，start、end均为 非负整数。若结束参数(end)省略，则表示从start位置一直截取到最后。

```javascript
var str = 'javascript';
console.log( str.substring(1, 4) ); //"ava"
console.log( str.substring(1) );  // "avascript"
```

### 5. slice()

```javascript
str.slice(start[,end])
```

作用：返回从 start 到 end （不包括）之间的字符，可传负值

```javascript
var str = 'this is awesome';
console.log( str.slice(1, 3) );  // "hi"
console.log( str.slice(10, -1) );  // "esom"
console.log( str.slice(10, -2) );  // "eso"
```

> 从最右边起，字母e为-1，m为-2,依次类推。

### 6. substr()

```javascript
str.slice(start[,length])
```

作用：返回 str 中从指定位置开始到指定长度的子字符串，start可为负值

```javascript
var str = "javascript";
console.log( str.substr(5, 3) );  // "cri"
console.log( str.substr(-4, 2) );  // "ri"
```

### 7. replace()

```javascript
str.replace(regexp|substr, newSubStr|function)
```

作用：替换 str 的子字符串

```javascript
//普通替换
var str = "i love you";
console.log( str.replace('love','hate') );  // "i hate you"

//正则替换
var tel = '13534566789'; 
var reg = /(\d{3})\d{4}(\d{4})/g;
console.log( tel.replace(reg,"$1****$2") );  // 135****6789

//驼峰转换
function strCovert(css){
		//定义一个正则尽可能找到我们要替换的内容
		var reg = /-([a-z])/g;
		var newStr = css.replace(reg,function($0,$1){
			//$0:代表正则匹配的结果
			//$1:代表正则匹配的第1个括号中的结果
			console.log('$0:',$0); // -b -c 
  			console.log('$1:',$1); // b  c 
			return $1.toUpperCase();
		});
		return newStr; 
}
var css = 'border-bottom-color'; 
console.log(strCovert(css)); //"borderBottomColor" 
```



### 8. search()

```javascript
str.search(regexp)
```

作用： 查找 str 与一个正则表达式是否匹配。如果匹配成功，则返回正则表达式在字符串中首次匹配项的索引,否则返回 -1。如果参数传入的是一个非正则表达式对象，则会使用 new RegExp(obj) 隐式地将其转换为正则表达式对象

```javascript
var str = 'I love JavaScript!';
console.log( str.search(/java/) ); // -1
console.log( str.search(/Java/) ); // 7
console.log( str.search(/java/i) ); // 7
console.log( str.search('Java') ); // 7
```

### 9. match()

```javascript
str.match(regexp)
```

作用：返回一个包含匹配结果的数组，如果没有匹配项，则返回 null。如果参数传入的是一个非正则表达式对象，则会使用 new RegExp(obj) 隐式地将其转换为正则表达式对象

```javascript
var str = 'Javascript java';
console.log( str.match(/Java/) ); // ["Java"]
console.log( str.match(/Java/g) ); // ["Java"]
console.log( str.match(/Java/gi) ); // ["java", "Java"]
console.log( str.match(/ab/g) ); // null
```

### 10. split()

```javascript
str.split([delimiter][, limit])
```

作用：返回一个数组，分隔符delimiter 可以是一个字符串或正则表达式

```javascript
var str = "Hello?World!";
console.log( str .split() ); // ["Hello?World!"]
console.log( str.split('?') ); // ["Hello", "World!"]
console.log( str.split('') ); // ["H", "e", "l", "l", "o", "?", "W", "o", "r", "l", "d", "!"]
console.log( str.split('',5) ); // ["H", "e", "l", "l", "o"]
console.log( str.split(/\?/) ); // ["Hello", "World!"]
```

### 11. trim()

```javascript
str.trim()
```

作用：去除 str 开头和结尾处的空白字符，返回 str 的一个副本，不影响字符串本身的值

```javascript
var str = '   a b c  ';
console.log( str.trim() );	// 'a b c'
console.log( str ); 	// '   abc  '
```

### 12. toLowerCase()

```javascript
str.toLowerCase()
```

作用：将 str 转换为小写，并返回 str 的一个副本，不影响字符串本身的值

```javascript
var str = 'JavaScript';
console.log( str.toLowerCase() ); // 'javascript'
console.log(str);  // 'JavaScript'
```

### 13. toUpperCase()

```javascript
str.toUpperCase()
```

作用： 将 str 转换为大写，并返回 str 的一个副本，不影响字符串本身的值

```javascript
var str = 'JavaScript';
console.log( str.toUpperCase() ); // 'JAVASCRIPT'
console.log(str);  // 'JavaScript'
```

### 14.repeat()

```javascript
str.repeat(length)
```

作用：重复一个str字符串length次

```javascript
console.log( '*'.repeat(3) ); //***
console.log( 'php'.repeat(3) ); //phpphpphp
```

### 15.concat()

```javascript
str.concat(value，...)
```

作用：将value与字符串str拼接在一起

```javascript
var str = 'JavaScript';
console.log( str.concat('php','mysql') ); // JavaScriptphpmysql
```








