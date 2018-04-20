---
title: 浅谈BFC
date: 2018-03-30 23:15:24
tags: CSS
category: CSS
---


## 一、什么是BFC（Block Formatting Context）
#### Box
Box 是 CSS 布局的对象和基本单位， 直观点来说，就是一个页面是由很多个 Box 组成的。元素的类型和 display 属性，决定了这个 Box 的类型。 不同类型的 Box， 会参与不同的 Formatting Context（一个决定如何渲染文档的容器），因此Box内的元素会以不同的方式渲染。

#### Formatting Context
Formatting context 是 W3C CSS2.1 规范中的一个概念。它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用。最常见的 Formatting context 有 Block fomatting context (简称BFC)和 Inline formatting context (简称IFC)。

CSS2.1 中只有 BFC 和 IFC, CSS3 中还增加了 GFC 和 FFC。

#### BFC
BFC(Block formatting context)直译为"块级格式化上下文"。它是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。

## 二、怎么触发BFC
 - body 根元素
 - 浮动元素：float 除 none 以外的值
 - 绝对定位元素：position (absolute、fixed)
 - display 为 inline-block、table-cell、table-caption、flex、inline-flex
 - overflow 除了 visible 以外的值 (hidden、auto、scroll)



## 三、参考链接
 - [前端精选文摘：BFC 神奇背后的原理（转）](https://www.w3ctech.com/topic/865)
 - [10 分钟理解 BFC 原理](https://zhuanlan.zhihu.com/p/25321647)
