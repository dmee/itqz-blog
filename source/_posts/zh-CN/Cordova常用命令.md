---
title: Cordova常用命令
date: 2018-01-30 23:15:24
tags:
    - Cordova
category: HyBrid
---
## 创建工程 
```javascript
cordova create projectName 
```
#### 案例
```javascript
cordova create projectName package Title
```
 - projectName 工程名称
 - package 反向域名值，类似于java包命名
 - Title 应用程序的标题
 
## 添加平台
```javascript
cordova platform add platformName
```
 - platformName 平台名称，android、ios、browser
 
## 移除平台
```javascript
cordova platform rm platformName
```

## 构建项目
```javascript
cordova build platformName
```

## 在模拟器上运行(前提是创建好AVD)
```javascript
cordova emulate platformName
```

## 在浏览器运行
```javascript
cordova serve android
```

## 编译和运行项目
```javascript
cordova run platformName
```

## 查看插件列表
```javascript
cordova plugin list
```

## 添加插件
```javascript
cordova plugin add PluginName
```

## 删除插件
```javascript
cordova plugin remove PluginName
```
