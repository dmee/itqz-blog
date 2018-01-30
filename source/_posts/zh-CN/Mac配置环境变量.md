---
title: Mac配置环境变量
date: 2018-01-30 23:09:38
tags:
    - Mac
category: basic
---
## 加载顺序
 - 1、 /etc/profile
 - 2、 /etc/paths 
 - 3、 ~/.bash_profile
 - 4、 ~/.bash_login
 - 5、 ~/.profile
 - 6、 ~/.bashrc

当然/etc/profile和/etc/paths是系统级别的，系统启动就会加载，后面几个是当前用户级的环境变量。后面3个按照从前往后的顺序读取，如果~/.bash_profile文件存在，则后面的几个文件就会被忽略不读了，如果~/.bash_profile文件不存在，才会以此类推读取后面的文件。~/.bashrc没有上述规则，它是bash shell打开的时候载入的。

## 设置PATH的语法
```bash
#中间用冒号隔开
export PATH=$PATH:<PATH 1>:<PATH 2>:<PATH 3>:------:<PATH N>
```

## 全局设置
下面的几个文件设置是全局的，修改时需要root权限

#### /etc/paths （全局建议修改这个文件 ）
编辑 paths，将环境变量添加到 paths文件中 ，一行一个路径
Hint：输入环境变量时，不用一个一个地输入，只要拖动文件夹到 Terminal 里就可以了。

#### /etc/profile （建议不修改这个文件 ）
全局（公有）配置，不管是哪个用户，登录时都会读取该文件。

#### /etc/bashrc （一般在这个文件中添加系统级环境变量）
全局（公有）配置，bash shell执行时，不管是何种方式，都会读取此文件。

## 单个用户设置

~/.bash_profile （任意一个文件中添加用户级环境变量）
（注：Linux 里面是 .bashrc 而 Mac 是 .bash_profile）
若bash shell是以login方式执行时，才会读取此文件。该文件仅仅执行一次!默认情况下,他设置一些环境变量。
设置命令别名
```bash
alias ll=’ls -la’
```
设置环境变量：
```bash
export PATH=/opt/local/bin:/opt/local/sbin:$PATH
```

**~/.bashrc 同上**

如果想立刻生效，则可执行下面的语句：
```bash
$ source 相应的文件
```
一般环境变量更改后，重启后生效。