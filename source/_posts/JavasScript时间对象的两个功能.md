---
title: JavasScript时间对象的两个功能
date: 2018-07-07 15:50:31
tags: 
	- JavaScript
	- Date
	- time

---


## 时间对象

- 创建基于当前时间的时间对象

```javascript
new Date();
```

- 基于传递的参数作为时间对象

```javascript
new Date(milliseconds); //milliseconds毫秒值

new Date(datestring); //一个字符串，声明了日期，也可以同时声明时间

new Date(year, month, day, hours, minutes, seconds, ms); //单独指定年、月、日、时、秒、毫秒
```



## 抢购倒计时

```javascript
//"剩余时间6天 2小时 28 分钟20 秒"
function getOverTime(endTime){
    var nowDate=new Date();  //开始时间，当前时间
    var endDate=new Date(endTime); //结束时间，需传入时间参数
    var t=endDate.getTime()-nowDate.getTime();  //时间差的毫秒数
    var d=0,h=0,m=0,s=0;
    if(t>=0){
      d=Math.floor(t/1000/3600/24);
      h=Math.floor(t/1000/60/60%24);
      m=Math.floor(t/1000/60%60);
      s=Math.floor(t/1000%60);
    } 
    return "仅剩："+d+"天"+h+"小时 "+m+"分钟"+s+"秒";
}

//每一秒延时执行getOverTime(date)
console.log( getOverTime('2018-04-20 15:30' ) ); // 仅剩：21天23小时 4分钟31秒
console.log( getOverTime('2018-03-30 12:30' ) ); // 仅剩：21天23小时 4分钟31秒
setInterval(function(){
    console.log( getOverTime('2018-04-28 15:30') )
},1000);
```

## 微信朋友圈发布的时间

```javascript
function release_time(date){
    var startDate = new Date(date); //把当前传入的时间转化为js时间对象
    var nowDate = new Date(); //创建一个当前的时间对象
    
    var cha=nowDate.getTime()-startDate.getTime(); //毫秒值差
    cha = Math.ceil(cha/1000);//毫秒转化为秒 

    var fenzhong=60;  // 一分钟秒数
    var xiaoshi=60*60; // 一小时秒数
    var tian=60*60*24;  // 一天的秒数 
    var yue=60*60*24*30;  // 一月的秒数 
    var nian=60*60*24*30*12;  // 一年的秒数 
    //2016年6月   2018年4月    50s   
    if(cha > nian){
         return Math.floor(cha/nian)+'年前';
    }else if(cha > yue ){
        return Math.floor(cha/yue)+'月前';
    }else if(cha > tian ){
        return Math.floor(cha/tian)+'天前';
    }else if(cha > xiaoshi){
        return Math.floor(cha/xiaoshi)+'小时前';
    }else{
       return Math.floor(cha/fenzhong)>0?Math.floor(cha/fenzhong):1+'分钟前';   
    }
}
console.log( release_time('2015-04-25 19:49') ); // 26分钟前
console.log( release_time('2018-03-30 10:35') ); // 26分钟前
console.log( release_time('2017-11-29 15:54') ); // 26分钟前
console.log( release_time('2018-03-28 23:42') ); // 17小时前
console.log( release_time('2018-04-24 17:42') ); // 4天前
console.log( release_time('2018-04-25 21:16') ); // 4天前
```


