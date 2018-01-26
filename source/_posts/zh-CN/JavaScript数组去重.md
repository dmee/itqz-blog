---
title: JavaScript数组去重
tags: JavaScript
category: JavaScript
date: 2018-01-26 17:04:12
---
## 方案一：利用数组的indexOf（一）

#### 原理

先声明一个空数组，然后循环数组成员，利用了数组的indexOf方法去判断当前成员是否存在新数组内，如果不存在则push进去，最后返回新数组得到一个去重后的数组！

**代码如下**

```javascript
Array.prototype.unique = function() {
    var newArr = [],
        i = 0,
        len = this.length;
    for (; i < len; i++) {
        var tempArr = this[i];
        if(newArr.indexOf(tempArr) === -1){
            newArr.push(tempArr);
        }
    }
    return newArr;
};
```


## 方案二：利用数组的indexOf方法（二）

#### 原理

创建一个新数组并插入第一个元素，再对数组进行轮询，判断当前元素在数组中的位置，如果不为 i 则表示在数组中已经存在，则不添加！

**代码如下：**

```javascript
Array.prototype.unique = function() {
    var newArr = [this[0]],
        i = 1,
        len = this.length;
    for (; i < len; i++) {
        var tempArr = this[i];
        if(this.indexOf(tempArr) === i){
            newArr.push(tempArr);
        }
    }
    return newArr;
};
```


## 方案三：利用对象的hash值

#### 原理：

创建一个obj对象，用于存放当前值得值，对数组进行轮询，判断当前值在obj对象中的值，如果不存在则添加！该方法利用了对象的hash进行了性能上的提升！相对前面两种该方法性能更高一点！

> 注意：当两个值一样，一个位数值类型，一个位字符串类型时，改方式要做改进。

**代码如下：**

```javascript
Array.prototype.unique = function() {
    var obj = {},
        newArr = [],
        i = 0,
        len = this.length;
    for (; i < len; i++) {
        var tempArr = this[i];
        if (!obj[tempArr]) {
            obj[tempArr] = true;
            newArr.push(tempArr);
        }
    }
    return newArr;
};
```
 

## 方案四：利用数组排序进行去重

#### 原理

先对数组进行排序，调用了数组内部的sort方法。然后对数组进行轮询，判断当前元素是不是新数组的最后一项，如果不是则表示是第一次添加，直接push进去，否则跳过。

**代码如下：**

```javascript
Array.prototype.unique = function() {
    this.sort();
    var newArr = [this[0]],
        i = 0,
        len = this.length;
    for (; i < len; i++) {
        var tempArr = this[i];
        if(tempArr !== newArr[newArr.length -1]){
            newArr.push(tempArr);
        }
    }
    return newArr;
};
```


## 方案五：利用正则匹配进行去重

#### 原理

先将数组转换成指定符号分割的字符串，然后进行一系列的替换操作，最后split成新的数组。（注意：原来数组成员类型为int的经过该操作后会变成string类型，慎用！！！！）

**代码如下：**

```javascript
Array.prototype.unique = function() {
    return this.sort().join(",,").replace(/(,|^)([^,]+)(,,\2)+(,|$)/g, "$1$2$4").replace(/,,+/g, ",").replace(/,$/, "").split(",");
}
```

## 方案六：利用Set进行去重
```javascript
function unique(arr){
    return Array.from(new Set(arr));
}

[...new Set()]
```

