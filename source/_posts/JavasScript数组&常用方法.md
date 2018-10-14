---
title: JavaScript数组&常用方法
date: 2018-07-07 15:45:27
tags: 
	- JavaScript
	- Array
---

### 数组

- 所谓数组，就是一些有顺序的数据集合（容器）,里面存放各种各样的数据。

  ```javascript
  var arr = ['a','b','c'];
  ```

- `length`属性
  可以用`length`属性取得数组(集合)的长度

  ```javascript
  var arr = ['a','b','c'];
  arr.length; // 3  返回3，说明数组有三个元素
  ```

- 数组下标

  数组中每个元素都有对应的标号指向它，这个标号我们可以称之为`下标`(索引)。

  下标从0开始，数组中的第1个元素下标为0，第2个元素下标为1，依次类推。 

  ```javascript
  var arr = ['a','b','c'];
  arr[0]; // 'a'
  arr[1]; // 'b'
  arr[2]; // 'c'
  ```

  > 当通过不存在的下标获取值则得到一个undefined值。

  ```javascript
  var arr = ['a','b','c'];
  arr[4]; // undefined
  ```

  



###  join()

```javascript
arr.join(separator)
```

作用：把数组中的每个元素用分隔符separator进行连接起来，返回一个字符串。如果省略了这个参数，默认使用逗号作为分隔符 

```javascript
var arr = ['a','b','c'];
console.log( arr.join('-') );  // 'a-b-c'
console.log( arr.join('') );  // 'abc'
console.log( arr.join() );  // 'a,b,c'
```

###  pop()

```javascript
arr.pop()
```

作用： 将删除arr的最后一个元素，把数组长度减1，并且返回它删除的元素的值。如果数组已经为空，则pop()不改变数组，返回undefined。 

```javascript
var arr = ['a','b','c'];

console.log( arr.pop() ); // c
console.log( arr.pop() ); // b
console.log( arr.pop() ); // a
console.log( arr.pop() ); // undefined
```

### push()

```javascript
arr.push(value,...)
```

作用：向数组尾部添加一个或多个元素 ，成功返回数组的新长度

```javascript
var arr = ['a','b','c'];
console.log( arr.push('d') ); // 4
console.log( arr.push('e','f') ); // 6
console.log(arr); //["a", "b", "c", "d", "e", "f"]
```

###  unshift()

```javascript
arr.unshift(value,...)
```

作用：向数组头部添加一个或多个元素 ，成功返回数组的新长度。

```javascript
var arr = ['a','b','c'];
console.log( arr.unshift('d') ); // 4
console.log( arr.unshift('e','f') ); // 6
console.log(arr); // ["e", "f", "d", "a", "b", "c"]
```

### shift()

```javascript
arr.shift()
```

作用：方法shift()将把arr的第—个元素移出数组，b并返回那个元素的值，并且将余下的所有元素前移一位，以填补数组头部的空缺 。

```javascript
var arr = ['a','b','c'];
console.log( arr.shift('d') ); // 'a'
console.log(arr); // ["b", "c"]
```

### sort()

```javascript
arr.sort(callback)
```

作用：对数组进行排序，指定d回调函数callback进行排序。

返回值：对数组的引用。注意，数组在原数组上进行排序，不制作副本。 

```javascript
var arr = [14,8,24];
arr.sort( function(a,b){ 
    return a-b; // 或return  a>b   
}) ;  
console.log(arr);  // [8, 14, 24]  升序

var arr = [14,8,24];
arr.sort(function(a,b){ 
        return b-a; //  或return b>a  
}) ;  
console.log(arr); //[24, 14, 8] 降序
```

###  slice()

```javascript
arr.slice(start,[,end])
```

作用：截取数组长度。从下标start开始，到end（不包括该元素）下标结束，

```javascript
var arr = [1,2,3,4,5];
console.log( arr.slice(2,4)); // [3,4]
```

若没有写end结束下标，则截取到数组末尾。

```javascript
var arr = [1,2,3,4,5];
console.log( arr.slice(2)); // [3,4,5]
```

若end为负数，则从数组尾部开始截取，即-1指最后一个元素，-2指倒数第二个元素，以此类推 。

> 注：不包括最后一个元素。

```javascript
var arr = [1,2,3,4,5];
console.log( arr.slice(2,-1)); // [3,4]
console.log( arr.slice(2,-2)); // [3]
```



###  toString()

```javascript
arr.toString()
```

作用： 把数组转为用逗号连接的字符串表示。类似`arr.join()`效果一样

```javascript
var arr = [1,2,3,4,5];
console.log( arr.toString() ); // '1,2,3,4,5'
console.log( arr.join() ); // '1,2,3,4,5'
```

###  splice()

```javascript
arr.splice(start, deleteCount, value, ...)
```

参数

- start

  开始插入和(或)删除的数组元素的下标 

- deleteCount

  从start开始，包括start所指的元素在内要删除的元素个数。这个参数是可选的，如果没有指定它，splice()将删除从start开始到原数组结尾的所有元素。 

- value

  要插人数组的零个或多个值，从start所指的下标处开始插入 

返回值

​	如果从arr中删除了元素，返回的是含有被删除的元素的数组。 



例1：从下标2开始删除后面所有的元素

```javascript
var arr = [1,2,3,4,5];
console.log( arr.splice(2) ); // [3,4,5]
console.log(arr);// [1,2]
```

例2：从下标2开始删除后面的2个元素


```javascript
var arr = [1,2,3,4,5];
console.log( arr.splice(2,2) ); // [3,4]
console.log(arr);// [1,2,5]
```

例3：从下标2开始删除后面的2个元素,同时在start指定的下标2后面加一个元素new

```javascript
var arr = [1,2,3,4,5];
console.log( arr.splice(2,2,'new') ); // [3,4]
console.log(arr);// [1,2,'new',5]
```



###  reverse()

```javascript
arr.reverse()
```

作用：颠倒数组中元素的顺序,返回新的电刀后的数组元素

```javascript
var arr = [1,2,3,4,5];
console.log( arr.reverse() ); // [5, 4, 3, 2, 1]
```

### isArray()

作用：检测一个变量是否是数组。（typeof不行,返回的是object）

```javascript
function isArray(value){
    return Object.prototype.toString.call(value) == '[object Array]';
}

var arr = [1,2,3,4,5];
console.log(isArray(arr)); // true
console.log(isArray({})); // false
```

同理：

​	判断是否是对象使用`[object object]`

​	是否是字符串 `[object string]`

​	以此类推


### concat()

作用：连接多个数组，返回新的数组 

```javascript
var arr1 = [1,2,3,4,5];
var arr2 = [6,7,8];
console.log( arr1.concat(arr2) ); // [1, 2, 3, 4, 5, 6, 7, 8]
```

### foreach()

作用：遍历数组元素 

```javascript
var arr = ['a','b','c'];
arr.forEach(function(v,key){
    //v当前循环的元素 key当前元素的下标
    console.log(key,v)
});
```

结果：

```
0 "a"
1 "b"
2 "c"
```

### filter()

作用：过滤数组中的某些元素，在回调函数中设置条件，不满足的都会被过滤掉，返回一个新数组。 

```javascript
var age = [18,23,28,30];
var newArr = age.filter(function(v){
    //v当前循环的元素
    //返回年龄大于25的元素
    return v>25;
});

console.log(newArr);// [28, 30]
```

### map()

作用：遍历数组，数组里的元素经过指定回调函数进行加工处理。  返回一个新的数组

```javascript
var age = [18,23,28,30];
var newArr = age.map(function(v){
    //给每个元素加10岁
    return v+10;
});
console.log(newArr); // [28, 33, 38, 40]
```
### reduce()

reduce方法有两个参数，第一个参数是一个callback，用于针对数组项的操作；第二个参数则是传入的初始值，这个初始值用于单个数组项的操作。需要注意的是，reduce方法返回值并不是数组，而是返回经过叠加处理后的结果。

reduce方法最常见的场景就是叠加 

```javascript
var items = [5,6,7];
var callback = function(sum,item){
    //item数组值的每个元素
    //sum每次累加的和
    return sum+item;
}

var total = items.reduce(callback,0); //把循环完后的累加结果加0
console.log(total); // 18
```

### 数组去重

方式有很多种。



- 用es6的Set对象

```javascript
var arr = [1,2,3,3,4,5,5];
var set = new Set(arr);
var newArr = Array.from(set);
console.log(newArr); // [1, 2, 3, 4, 5]
```
更骚气的用法：

```javascript
var newArr = [...new Set([1,2,3,3,4,5,5])]
console.log(newArr); // [1, 2, 3, 4, 5]
```

- 另indexOf方法来判断，存在返回元素下标，不存在返回-1

建立一个存放结果的数组，利用indexOf判断是否存在于新数组中，不存在则push到新数组，最后返回新数组 

```javascript
var unique = function(arr) {
    var n = []; // 存放已遍历的满足条件的元素
    for (var i = 0; i < arr.length; i++) {
        // indexOf()判断当前元素是否已存在
        if (n.indexOf(arr[i]) == -1) n.push(arr[i]);
    }
    return n;
}

var arr = [1,2,2,3,3,4,5];
console.log( unique(arr) ); // [1, 2, 3, 4, 5]
```

如果想arr.unique()这样调用，则需要把此方法加上Array的原型对象上。

```javascript
Array.prototype.unique = function() {
    var n = []; // 存放已遍历的满足条件的元素
    for (var i = 0; i < this.length; i++) {
        // indexOf()判断当前元素是否已存在
        if (n.indexOf(this[i]) == -1) n.push(this[i]);
    }
    return n;
}
var arr = [1,2,3,3,6,6];
console.log( arr.unique() );  // [1, 2, 3, 6]

```

### 数组中是否存在于某个值

可以用indexOf方法来判断，存在返回元素下标，不存在返回-1

```javascript
function inArray(value,arr){
    return arr.indexOf(value)!== -1 ? true : false;
}
var arr = [1,2,3];
console.log( inArray(2,arr) ); // true
console.log( inArray(4,arr) ); // false
```


由于笔者才学疏浅，文章有错误的地方望大家批评指正，一起学习进步。
