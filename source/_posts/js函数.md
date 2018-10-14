---
title: js函数
date: 2018-09-18 16:26:12
tags:
	- JavaScript
	- 函数
---



# 函数

## 什么是函数？

简单说，就是实现某个功能的代码片段，可以提高代码的复用性。



## 函数的分类

- 内置函数
- 自定义函数



## 创建函数

常见的有两种创建函数的形式：

- 通过函数声明（也叫函数定义）如：function fnName(){}

- 通过函数表达式。如：var fnName = function(){}

  

### 创建方式一：函数声明

```javascript
function 函数名([形参列表]){
	// 函数体
}

//函数调用
函数名([实参列表]);
```

说明：

- 上面定义函数的方式称之为`函数定义或函数声明`

- function它是定义函数的关键字 不可以省略 
- 函数名命名规则与变量名是一样的
- 定义多个同名函数后者覆盖前者
- 不能使用JS中的关键字和保留字作为函数名
- 函数名后面紧跟着小括号里面可能有参数，我们称之为形参，调用时传递的参数叫实参。
- 花括号{}里面是函数体

例1：定义一个名为sayHello的函数。

```javascript
function sayHello(){
    return 'hello';
}

//调用
console.log( sayHello() ); // hello
```



例2：定义一个名为add的求和函数

```javascript
function add(num1,num2){
	return num1+num2;
}

//调用
console.log( add(100,200) ); // 300
```



> **注意：**在定义函数时如果有形参 ， 在调用的时候也要传递对于实参，但是这个不是绝对的！

 ### 创建方式二：函数表达式

1. 语法：

```javascript
var fnName = function(){}
```

说明：

- 相当于定义了一个没有函数名的函数，我们称之为匿名函数。
- 把匿名函数的地址引用赋值给变量fnName。fnName相当于函数的名字，通过fnName后面加小括号`()`就可以调用此函数。



例：把一个匿名函数赋给变量add

```javascript
//把匿名函数的地址引用赋值给变量add,add相当于函数的名字
var add = function(num1,num2){
    return num1+num2;
}
//调用
console.log( add(100,200)  );
```



注意：下面定义的匿名函数若在function后面加函数名，再通过这个函数名访问是无效的，会报错。

```javascript
  var add = function myadd(num1,num2){
      return num1+num2;
  }
  //调用
  console.log( add(100,200)  ); // 300
  console.log( myadd(200,300)  ); //报错 Uncaught ReferenceError: myadd is not defined
```



2. **匿名函数应用场景**

**匿名函数在JS中使用是最多的**,如在js事件中，多数会把匿名函数赋给一个事件名。如单击事件

```javascript
btn.onclick = function(){
    alert('被单击了');
}
```

将匿名函数赋值给事件，那么匿名函数什么时候才会执行？它要等到事件触发了以后才会执行。

> 当然，以后匿名函数还会有更多的应用场景。









## 函数返回值return

一般在函数体中会有`return`关键字，来将函数的处理结果返回给调用者。

```javascript
function add(num1,num2){
	return num1+num2;
}

//使用变量num来接收函数的返回结果
var sum = add(100,200); 
console.log( sum ); // 300
```

注意：

- 函数有return返回，调用者一定要用变量接收，不接受否则return返回就没意义。
- 函数没有return关键字，则默认返回`undefined`。
- 当函数体里面遇到了return关键字以后，当前的这个函数就不会再往下进行执行了。





 





  



 # 函数的自执行(自调用)



## 定义方式



常见的有以下两种定义方式：

```javascript
 方式一： (function([形参列表]){})([实参列表]);  // 括号在外面
 方式二： (function([形参列表]){}([实参列表]));	// 括号在里面
```

区别：后面的实参小括号()一个在外面一个在里面，两者一样，没有本质的区别。

## 函数的自执行作用

多用于模块化编程，封装js插件使用较多。

如知名的jQuery库就是使用此方法，就是让此库中的代码自己执行一遍，可以实现相应的功能）



**示例代码**：

```javascript
(function(a,b){
    console.log(a,b);
})(100,200)；
```

或：

```javascript
(function(a,b){
    console.log(a,b);
}(100,200))；
```

执行结果都是300。



**注意**

当在一个js文件中，如果js代码过多，可能会出现某行代码没有加`分号;`结束,导致代码压缩的时候就会报错。 

压缩：会把所有代码的空格、换行符和空白字符都去掉，容量更小，网络间传输速度更快。压缩过的js文件会带`min`字样。

所以一般建议这样写：

```javascript
;(function(a,b){
    console.log(a,b);
})(100,200)；
```

> js语句后面不加分号不会报错，代码依然可以执行，那是因为js引擎会自动在语句后面添加分号，但这不是一个好的习惯。



# 函数的内部属性arguments

## arguments作用

**arguments**是用于函数内获取实参列表的集合，它是一个数组。



注意：因为在js函数中，定义函数时没有定义形参，但是调用函数的时候传递了实参，由于没有形参获取不到对于的实参值，这时就可以通过**arguments**来获取实参的值。



示例代码：

```javascript
function test(){
    console.log(arguments); // [100,200]
}
test(100,200);
```

> 注：arguments只能在函数内部使用。

 

## arguments应用场景

我们知道，当函数没有定义形参的时候，此时可以通过`arguments.length`来获取实参的个数和值，有时候我们的函数功能可以根据`传递实参个数`从而实现不同的功能。如后面我们会学习jQuery库，其中有个css的方法如下: 

- 传递`一个参数`就是获取对应值：css(‘width’) 获取宽度值
- 传递`两个参数`就是设置对应的值：css(‘width’,’100px’) 设置宽度值为100px

```javascript
function css(){
    //获取实参的个数
    alert(arguments.length); 
}

css('width'); // 弹出 1
css('width','100px'); // 弹出 2
```

## arguments实现求和函数

**需求**：传递不同个数的数，把这些数进行求和返回

示例代码：

```javascript
function add(){
	var sum = 0;
    for(var i=0; i<arguments.length; i++){
    	sum += arguments[i];
    }
    //返回和
    return sum;
}

console.log( add(100,200) );  // 300
console.log( add(100,200,300) ); // 600
```



# 高阶函数

## 定义

 高阶函数是指至少满足以下条件之一的函数：

1.函数作为参数被传递

2.函数可以作为返回值



- 第一种情况：函数作为参数被传递

```javascript
function foo(callback){
	//callback为函数，执行后面加小括号
	callback();
}
//调用
foo(function(){
	console.log('执行了');
});
```



注意：执行回调函数callback的时候，如果传递了实参，则传递函数的时候也要定义形参来接受，如下：

```javascript
function add(a,b,callback){
	//callback为函数，执行后面加小括号
	callback(a+b);
}

add(100,200,function(result){
    console.log(result); // 300
});
```



- 第二种情况：函数作为返回值

```javascript
function foo(callback){
	return callback;
}

// fn变量就是指向callback函数
var fn = foo(function(){
	console.log('执行了');
});

fn(); // 执行了
```





## 高阶函数的作用

答：一般是业务逻辑较多的时候，我们就可以把这些逻辑直接封装在一个函数中，再把此函数作为参数传递给另外一个函数帮我们去执行这些逻辑。

所谓的函数式编程就是指这种高度抽象的编程范式。多数用于封装更加复杂的功能。



## 具体运用

```javascript
var add = function(a,b){
    return a + b;
};
function math(func,arr){
    return func(arr[0],arr[1]);
}

var sum = math(add,[1,2]) ;
console.log(sum); // 3

```

上面的例子函数math中传进去的是一个add函数，其return返回的结果就是add函数执行的结果。







 

 

 

 

 


