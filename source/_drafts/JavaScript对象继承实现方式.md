---
title: JavaScript对象继承实现方式
date: 2018-02-25 11:16:54
tags: JavaScript
category: JavaScript
---

## 一、原型链继承
### 基本思想
利用原型让一个引用类型继承另外一个引用类型的属性和方法。（拿父类实例来充当子类原型对象）

### 实现方式
```javascript
// 父类
function SuperClass(){
    this.name = 'super class';
    this.list = [1];
}
SuperClass.prototype.getClassName =  function(){
    return this.name;
}

// 子类
function SubClass(){
    this.name = 'sub class';
}
SubClass.prototype = new SuperClass();

var subInstance = new SubClass();
console.info(subInstance.getClassName()); // sub class

// 缺点如下
var sub_1 = new SubClass(),
    sub_2 = new SubClass();
sub_1.list.push(2);
console.info(sub_1.list); // [1, 2]
console.info(sub_2.list); // [1, 2]

```

### 优缺点
**优点**
 - 简单易实现

**缺点**
 - 多个子类实例操作父类实例的引用类型属性时，数据并不会隔离，出现共享内存，数据串掉的情况。
 - 在创建子类实例时无法向父类构造函数传递参数

## 二、构造函数继承(经典继承)
### 基本思想
在子类的构造函数内部通过call、apply方法“借调”调用超类的构造函数。

### 实现方式
```javascript
function SuperClass(name){
    this.name = name;
}

function SubClass(name){
    SuperClass.call(this, name);
}
var sub_1 = new SubClass('niki');
console.info(sub_1.name);
```

### 优缺点
**优点**
 - 创建子类的时候，可以向父类构造函数传递参数

**缺点**
 - 访问不到父类的原型链中的方法和属性

## 三、组合继承(伪经典继承)
### 基本思想
将原型链继承与构造函数继承两者继承方式的优点结合在一起，通过原型链继承来继承父类的原型链上的属性与方法，通过构造函数继承来实现实例属性的继承，这样既能保证函数的复用性，又能保证每个实例都有自己的属性。
### 实现方式
```javascript
function SuperClass(name) {
    this.name = name;
    this.list = [1];
}
SuperClass.prototype.sayName = function() {
    console.info(this.name);
}

function SubClass(name, age) {
    SuperClass.call(this, name);
    this.age = age;
}
SubClass.prototype = new SuperClass();
SubClass.prototype.constructor = SubClass;
SubClass.prototype.sayAge = function() {
    console.info(this.age);
}

var sub_1 = new SubClass('bob', 18);
sub_1.sayName(); // bob
sub_1.sayAge(); // 18
sub_1.list.push(2);
console.info(sub_1.list); // [1, 2]


var sub_2 = new SubClass('niki', 20);
sub_2.sayName(); // niki
sub_2.sayAge(); // 20
console.info(sub_2.list); // [1]
```


## 四、原型式继承
### 基本思想
借助原型可以基于已有的对象创建新对象，同时还不必因此创建自定义类型。（对象的浅拷贝）

### 实现方式
```javascript
function extend(obj) {
    function F() {}
    ;F.prototype = obj;
    return new F();
}

var Person = {
    name: 'niki',
    friends: ['Bob', 'Alice']
}
var p_1 = extend(Person);
p_1.friends.push('Jim');
console.info(p_1.friends); // ["Bob", "Alice", "Jim"]


var p_2 = extend(Person);
p_2.friends.push('Tom');
console.info(p_2.friends); // ["Bob", "Alice", "Jim", "Tom"]
```

### 优缺点
**优点**
 - 简单粗暴

**缺点**
 - 会跟原型链继承一样有引用类型值共享的问题

## 五、寄生式继承

## 六、寄生组合式继承

## 参考文章
 - JavaScript高级程序设计 6.3

