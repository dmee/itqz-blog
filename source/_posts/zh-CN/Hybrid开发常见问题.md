---
title: Hybrid开发常见问题
date: 2018-01-30 10:13:42
tags:
category:
---

## 1、页面初始化input表单在focus时隐藏软键盘(以JQuery为例)
### 场景
用SPA架构开发Hybrid应用时，当用户与应用进行交互后，会导致页面初始化聚焦时弹出软键盘，严重影响用户体验（开发的APP为PDA应用时，需要自动聚焦用于扫描数据）
### 实现原理
 - 当input设置为readonly时，不会调出软键盘，且还会有光标
 - 当input设置为disabled时，虽然不会调出软键盘，但是没有光标，用户体验不及readonly

### 解决方案
```javascript
$dom.attr('readonly', 'readonly').focus().removeArrt('readonly');
```

