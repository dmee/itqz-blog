---
title: JavaScript中Attribute与Property的区别
date: 2018-01-30 10:13:42
tags: JavaScript
category:  JavaScript
---
## 一、基本用法
### 1.Attribute
```javascript
var dom = document.getElementById('#id');
console.info(dom.attributes); // 打印所有节点属性

// 设置属性
dom.setAttribute('attrName', 'attrValue');

// 获取属性
dom.getAttribute('attrName');

// 删除属性
dom.removeAttribute('attrName');
```

### 2.Property

## 二、两者的区别
 - 1.两者在词面上都是属性的意思，但是Attribute更倾向于HTML的标签节点上的可见的属性，它的值只能是字符串；Property更倾向于DOM对象的属性，它是JavaScript的一个对象，值的类型不局限于字符串。
 - 2.

## 参考
 - 1.[http://javascript.info/dom-attributes-and-properties](http://javascript.info/dom-attributes-and-properties)
