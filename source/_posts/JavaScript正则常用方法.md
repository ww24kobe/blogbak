---
title: JavaScript正则常用方法
date: 2018-07-09 01:05:02
tags: 
	- 正则
---

正则常用的一些方法

## 1. test()

    regexp.test(str)

作用： 检测一个字符串是否匹配某个正则。满足返回true,否则返回false。此方法的返回结果会受到是否加全局标志`g`的影响

未加全局g测试代码：

    var regexp = /^1[3-9]\d{9}$/; // 手机号正则
    console.log( regexp.lastIndex ); // 0 
    console.log( regexp.test('13588888888') ); // true
    console.log( regexp.lastIndex ); // 0 
    console.log( regexp.test('18588888888') ); // true
    console.log( regexp.lastIndex ); // 0
    console.log( regexp.test('12588888888') ); // false 第2位不满足

`lastIndex`属性是正则下次往后匹配的起始位置
可见，未加全局g,则lastIndex属性值一直从0开始往后匹配。


加全局g测试代码：

```javascript
var regexp = /^1[3-9]\d{9}$/g;

console.log( regexp.lastIndex ); // 0   默认从下标0向后匹配
console.log( regexp.test('13588888888') ); // true

console.log( regexp.lastIndex ); // 11 后面往后匹配的下标位置
console.log( regexp.test('13588888888') ); // false

console.log( regexp.lastIndex); // 0 上面匹配失败下标重置为0
console.log( regexp.test('13588888888') ); // true

//如此循环着此过程
```

可见，加全局g的时候，lastIndex属性的值会受到test方法的影响。导致每次往后匹配的下标值是不一样的，若多次调用test方法会重复上面的过程。


若想每次都从下标0开始往后匹配，只需调用test前把lastIndex属性重置为0即可。
```javascript
regexp.lastIndex  = 0 ; // 重置为0
console.log( regexp.test('13588888888') ); // true
```

> 所以一般判断一个字符串是否满足一个正则，即对于结果是true或false的情况，此时正则建议不加全局g,这可让lastIndex属性每次都是从0开始向后匹配。



## 2. exec()

    regexp.exec(str)

作用： 返回正则匹配的结果，以一个数组返回 。此数组第一个元素（下标0）是正则相匹配的字符串，后面的下标元素依次是括号中捕获组匹配的内容。未匹配到则返回`null`



此方法和test一样，其返回结果都会受到正则全局标识`g`的影响。

未全局g测试：

    var regexp = /(\d{3})\d{4}(\d{4})/; 
    regexp.exec('13588888888') ; // ["13588888888", "135", "8888", index: 0, input: "13588888888"]
    regexp.lastIndex; // 0
    regexp.exec('13588888888') ; // ["13588888888", "135", "8888", index: 0, input: "13588888888"]
    regexp.lastIndex; // 0
    regexp.exec('13588888888') ; // ["13588888888", "135", "8888", index: 0, input: "13588888888"]

可见，匹配的结果都是一样的，结果为：`[13588888888'，'135'，'8888']`
下标`0`为1358888888是正则匹配的结果。
下标`1`为135是正则第`1`个捕获组匹配的结果。
下标`2`为8888是正则第`2`个捕获组匹配的结果。
...
多个捕获组的匹配结果以此类推




加全局g测试：
```javascript
    var regexp = /(\d{3})\d{4}(\d{4})/g; 
    regexp.lastIndex; // 0
    regexp.exec('13588888888'); // ["13588888888", "135", "8888",   index: 0, input: "13588888888"]
    regexp.lastIndex; // 11
    regexp.exec('13588888888'); // null
    regexp.lastIndex; // 0
    regexp.exec('13588888888'); // ["13588888888", "135", "8888", index: 0, input: "13588888888"]
```
结果和上面未加g代码测试结果一样，只是每次调用exec方法，其正则对象lastIndex属性值的下次起始匹配位置都会改变，这个变化和test方法是一样的。


### while循环exec方法
当正则加了全局标识g时，若要使用exec方法获取正则匹配的所有结果，一次次调用exec显然不行的，因为匹配成功就会停止，再次通过lastIndex属性的下标值继续往后匹配，因此不知道要调用多少次exec方法才可获得匹配的所有结果，一般做法是使用while循环exec方法，直到未匹配为止。 
如下：
```javascript
var str = '13423455678php18912345678';
var reg = /(\d{3})\d{4}(\d{4})/g;
var result = [];
var row;
while( row = reg.exec(str)){
    result.push(row);
}

console.log( result );
```
结果：
![image.png](https://upload-images.jianshu.io/upload_images/11273713-d927b1fe443ee8ef.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


