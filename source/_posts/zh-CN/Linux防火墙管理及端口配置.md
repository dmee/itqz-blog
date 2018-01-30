---
title: Linux防火墙管理及端口配置
tags: 
    - Linux
categories: Linux
date: 2018-01-26 14:36:38
---

## 防火墙开关（重启后生效）
 - 开启：chkconfig iptables on
 - 关闭：chkconfig iptables off
 
## 防火墙开关（即时生效，重启后失效）
 - 开启：service iptables start
 - 关闭：service iptables stop
 
## 配置端口开放
```bash
vim /etc/sysconfig/iptables

-A INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT
-A INPUT -p tcp -m state --state NEW -m tcp --dport 3306 -j ACCEPT
```