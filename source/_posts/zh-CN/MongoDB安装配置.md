---
title: MongoDB安装配置
date: 2018-01-30 23:20:33
tags:
    - MongoDB
category: MongoDB
---

## 查看MongoDB占用端口
```bash
netstat -apn | grep mongod
```

## 杀进程
```bash
kill -9 [pid]
```

## 查看日志文件
```bash
tail /mongodb/log/mongod.log
```

## 查看MongoDB配置文件
```bash
vim /mongodb/conf/mongod.conf
```

## 启动MongoDB
```bash
cd /etc/init.d/
mongod --dbpath /mongodb/ --auth
```

## 启动指定配置文件
```bash
cd /etc/init.d/
mongod --config /mongodb/conf/mongod.conf
```