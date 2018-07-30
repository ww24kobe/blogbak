---
title: php中的trait机制提高代码复用
date: 2018-07-09 01:10:10
tags:
	- php

---



# 什么是trait

自 PHP 5.4.0 起，PHP 实现了一种代码复用的方法，称为 trait。

Trait 是为类似 PHP 的单继承语言而准备的一种代码复用机制。Trait 为了减少单继承语言的限制，使开发人员能够自由地在不同层次结构内独立的类中复用 method。Trait 和 Class 组合的语义定义了一种减少复杂性的方式，避免传统多继承和 Mixin 类相关典型问题。

Trait 和 Class 相似，但仅仅旨在用细粒度和一致的方式来组合功能。 无法通过 trait 自身来实例化。它为传统继承增加了水平特性的组合；也就是说，应用的几个 Class 之间不需要继承。

其实就是一句话，弥补了php不能多继承的问题

# trait和当前类
```php
trait Goods {
	public function goodsInfo(){
		echo 'trait-goodsInfo';
	}
}

class c {
	use Goods;  // 相当与trait Goods给引入当前类，就可以使用其中的goodsInfo方法
	public function goodsAttr(){
		echo  'goodsAttr';
	}
}

$c = new c();
echo $c->goodsInfo(); // 'trait-goodsInfo'   
echo $c->goodsAttr(); // 'goodsAttr'
```

可见，对象调用一个方法若找不到，就会去当前类引入的trait中去找.

当类c中如果和引入的trait中有同名的方法，则优先会读取当前c中的方法，如下所示：

```php
trait Goods {
	public function goodsInfo(){
		echo 'trait-goodsInfo';
	}
}

class c {

	use Goods; //  相当与trait Goods给引入当前类，就可以使用其中的goodsInfo方法
	public function goodsAttr(){
		echo  'goodsAttr';
	}
	public function goodsInfo(){
		echo  'c-goodsInfo';
	}
}

$c = new c();
echo $c->goodsInfo(); // 'c-goodsInfo'
echo $c->goodsAttr(); // 'goodsAttr'

```

结果是`'c-goodsInfo'`.可见，当前类的优先级高于trait.

# trait和继承

```php
trait Goods {
	public function goodsInfo(){
		echo 'trait-goodsInfo';
	}
}

class p{
	public function goodsInfo(){
		echo 'p-goodsInfo';
	}
}

class c extends p{

	use Goods; //  相当与trait Goods给引入当前类，就可以使用其中的goodsInfo方法

}

$c = new c();
echo $c->goodsInfo(); // 'trait-goodsInfo'

```

结果是`'trait-goodsInfo'` ,可见trait的优先级高于继承。

# trait中的this
```php
trait Good{
	public function getName(){
		echo  "My name is " . $this->name;
	} 
}

class Person{
	public $name = '王大锤';
	use Good;
}
$p = new Person();
$p->getName(); // My name is 王大锤
```
可见，trait中的this依然是当前调用的对象p。

# trait中使用trait
```php
trait Hello {
	public function sayHello(){
		echo 'Hello';
	}
}

trait World {
	public function sayWorld(){
		echo 'World';
	}
}

trait HelloWorld {
	//使用多个trait
	use Hello,World;
}

class MyHelloWorld{
	use HelloWorld;
}

$obj = new MyHelloWorld();
$obj->sayHello(); // Hello 
$obj->sayWorld(); // World
```


关于trait的用法先介绍这么多吧！ 更多细节请看官网[trait](http://www.php.net/manual/zh/language.oop5.traits.php)的解释

# 小结 
* Trait 无法如 Class 一样使用 new 实例化
* 在单个 Class 中，可以使用多个 Trait 
* 当前类的优先级高于trait，trait的优先级高于继承。 `当前类>trait>继承类`
* 使用trait时候应该坚决避免命名冲突，尤其是同时使用多个trait时。
