layout: js的this、__proto__
title: JS的this、__proto__ 和. prototype 、constructor
date: 2016-12-22 10:54:10
tags:
- JavaScript
---

## 一、this关键字

### 作为函数被调用

>函数也可以直接被调用，此时 this 绑定到全局对象。在浏览器中，window 就是该全局对象。比如下面的例子：函数被调用时，this 被绑定到全局对象，接下来执行赋值语句，相当于隐式的声明了一个全局变量，这显然不是调用者希望的。

```javascript
function makeNoSense(x) { 
	this.x = x; 
} 

makeNoSense(5); 
x;// x 已经成为一个值为 5 的全局变量

```
<!--more-->

### 作为对象方法调用

>在 JavaScript 中，函数也是对象，因此函数可以作为一个对象的属性，此时该函数被称为该对象的方法，在使用这种调用方式时，this 被自然绑定到该对象。

```javascript
var point = { 
x : 0, 
y : 0, 
	moveTo : function(x, y) { 
		this.x = this.x + x; 
		this.y = this.y + y; 
	} 
}; 

point.moveTo(1, 1)//this 绑定到当前对象，即 point 对象

```
**内部函数再定义内部函数**

上述的moveTo()函数已经是point的内部函数了，如果，我还想在moveTo中再加入一个函数：

```javascript
var point = { 
	x : 0, 
	y : 0, 
	moveTo : function(x, y) {
		console.log(this); //point对象
		// 内部函数
		var moveX = function(x) {
		console.log(this); //window对象
		this.x = x;//this 绑定到了哪里？
	}; 
	// 内部函数
	var moveY = function(y) { 
		this.y = y;//this 绑定到了哪里？
	}; 

	moveX(x); 
	moveY(y); 
	} 
}; 
point.moveTo(1, 1); 
point.x; //==>0
point.y; //==>0
x; //==>1
y; //==>1

```
这里出现了一个错误，第一个this显示出是point对象，但是第二个this却显示出是window对象。

>这属于 JavaScript 的设计缺陷，正确的设计方式是内部函数的 this 应该绑定到其外层函数对应的对象上，为了规避这一设计缺陷，聪明的 JavaScript 程序员想出了变量替代的方法，约定俗成，该变量一般被命名为 that。

```javascript
var point = { 
	x : 0, 
	y : 0, 
	moveTo : function(x, y) { 
		var that = this; 
		// 内部函数
		var moveX = function(x) { 
			that.x = x; 
		}; 
		// 内部函数
		var moveY = function(y) { 
			that.y = y; 
		} 
		moveX(x); 
		moveY(y); 
	} 
}; 
point.moveTo(1, 1); 
point.x; //==>1 
point.y; //==>1

```
当内部函数嵌套只有一层，那么还是符合`内部函数this绑定在外层函数对应的对象上`，但是，如果超过了1层嵌套，那么在高于1层的内部函数中，this对象如果不借助that，那么this将会指向window对象。

### apply或call调用
﻿
```javascript
function Point(x, y){ 
	this.x = x; 
	this.y = y; 
	this.moveTo = function(x, y){ 
	    this.x = x; 
	    this.y = y; 
	} 
}

var p1 = new Point(0, 0); 
var p2 = {x: 0, y: 0}; 
p1.moveTo(1, 1); 
p1.moveTo.apply(p2, [10, 10]);

```
这里p1是一个`Point {x: 1, y: 1}`对象，而p2则是一个`Object {x: 10, y: 10}`对象。

### eval调用

>JavaScript 中的 eval 方法可以将字符串转换为 JavaScript 代码，使用 eval 方法时，this 指向哪里呢？答案很简单，看谁在调用 eval 方法，调用者的执行环境（ExecutionContext）中的 this 就被 eval 方法继承下来了。


## 二、__proto__ 和. prototype

>p.__proto__ === p.constructor.prototype === Person.prototype;

**一、 所有构造器/函数的__proto__都指向Function.prototype，它是一个空函数（Empty function）**

```javascript
function A(){}
A.__proto__ === Function.prototype; //true
//内置对象
Number.__proto__ === Function.prototype  // true

```
特殊的，如Math对象的_proto_是Object.prototype

```javascript
Math.__proto__ === Object.prototype  // true
```
>知道了所有构造器（含内置及自定义）的__proto__都是Function.prototype，那Function.prototype的__proto__是谁呢？
```javascript
Function.prototype.__proto__ === Object.prototype;//true

```
>这说明所有的构造器也都是一个普通JS对象，可以给构造器添加/删除属性等。同时它也继承了Object.prototype上的所有方法：toString、valueOf、hasOwnProperty等。

最后Object.prototype的__proto__是谁？

```javascript
Object.prototype.__proto__ === null  // true

```
**二、所有对象的__proto__都指向其构造器的prototype**

`__proto__`指向了，我不知道怎么说，用java的话来说就是class类。

```javascript
var obj = {name: 'jack'}
var arr = [1,2,3]
var reg = /hello/g
var date = new Date
var err = new Error('exception')
 
console.log(obj.__proto__ === Object.prototype) // true
console.log(arr.__proto__ === Array.prototype)  // true
console.log(reg.__proto__ === RegExp.prototype) // true
console.log(date.__proto__ === Date.prototype)  // true
console.log(err.__proto__ === Error.prototype)  // true

```
再看看自定义的构造器，这里定义了一个Person

```javascript
function Person(name) {
    this.name = name
}
var p = new Person('jack')
console.log(p.__proto__ === Person.prototype) // true

```
>p是Person的实例对象，p的内部原型总是指向其构造器Person的prototype。


每个对象都有一个constructor属性，可以获取它的构造器，因此以下打印结果也是恒等的

```javascript
function Person(name) {
    this.name = name
}
var p = new Person('jack')
p.__proto__ === p.constructor.prototype

```
### 修改原型

```javascript
function Person(name) {
    this.name = name
}
var p = new Person('jack')
Person.prototype = {
	getName: function() {}
}

```
又由于

```javascript
p.__proto__ === p.constructor.prototype === Person.prototype;

```
所以，我觉得有三种写法。

```javascript
Person.prototype.getName = function(){};
var per = new Person('jack');
per.__proto__.getName = function(){};
per.constructor.prototype.getName = function(){};

```
## 三、constructor属性

>返回一个指向创建了该对象原型的函数引用。

```javascript
var a,b;
(function(){
	function A (arg1,arg2) {
		this.a = 1;
		this.b=2; 
	}

	A.prototype.log = function () {
		console.log(this.a);
	}
	a = new A();
	b = new A();
})()
a.log();
// 1
b.log();
// 1

```
>通过以上代码我们可以得到两个对象，a,b，他们同为类A的实例。因为A在闭包里，所以现在我们是不能直接访问A的，那如果我想给类A增加新方法怎么办？

```javascript
// a.constructor.prototype 在chrome,firefox中可以通过 a.__proto__ 直接访问
a.constructor.prototype.log2 = function () {
	console.log(this.b)
}

a.log2();
// 2
b.log2();
// 2
```
由于闭包的特性，我们只能借助`a.constructor.prototype`来更改原型。

## 参考

<a href="https://www.ibm.com/developerworks/cn/web/1207_wangqf_jsthis/">https://www.ibm.com/developerworks/cn/web/1207_wangqf_jsthis/</a>
<a href="http://www.cnblogs.com/snandy/archive/2012/09/01/2664134.html">http://www.cnblogs.com/snandy/archive/2012/09/01/2664134.html</a>
<a href="http://stackoverflow.com/questions/9959727/proto-vs-prototype-in-javascript">http://stackoverflow.com/questions/9959727/proto-vs-prototype-in-javascript</a>