---
title: HTTP请求过程
tags: 
    - http
categories: basic
date: 2018-01-26 14:36:38
---

## 一、常见位码（TCP标志位）
 - 1.SYN：synchronous 建立联机
 - 2.ACK：acknowledgement 确认
 - 3.PSH：push 传送
 - 4.FIN：finish 结束
 - 5.RST：reset 重置
 - 6.URG：urgent 紧急

## 二、过程
 - 1.建立TCP连接（三次握手）
 - 2.数据传输
 - 3.断开TCP连接（四次挥手）


## 三、三次握手
![](/static/images/basic/http-connect.jpg)
### 请求过程
 - 1、第一次握手：主机A发送位码为syn＝1,随机产生seq number=1234567的数据包到服务器，主机B由SYN=1知道，A要求建立联机；
 - 2、第二次握手：主机B收到请求后要确认联机信息，向A发送ack number=(主机A的seq+1),syn=1,ack=1,随机产生seq=7654321的包
 - 3、第三次握手：主机A收到后检查ack number是否正确，即第一次发送的seq number+1,以及位码ack是否为1，若正确，主机A会再发送ack number=(主机B的seq+1),ack=1，主机B收到后确认seq值与ack=1则连接建立成功。

### 握手链路
在TCP/IP协议中，TCP协议提供可靠的连接服务，采用三次握手建立一个连接。 
 - 1、第一次握手：建立连接时，客户端发送syn包(syn=j)到服务器，并进入SYN_SEND状态，等待服务器确认； 
 - 2、第二次握手：服务器收到syn包，必须确认客户的SYN（ack=j+1），同时自己也发送一个SYN包（syn=k），即SYN+ACK包，此时服务器进入SYN_RECV状态； 
 - 3、第三次握手：客户端收到服务器的SYN＋ACK包，向服务器发送确认包ACK(ack=k+1)，此包发送完毕，客户端和服务器进入ESTABLISHED状态，完成三次握手。

## 四、四次挥手
![](/static/images/basic/http-disconnect.gif)

## 五、完整过程
![](/static/images/basic/http-connect.gif)

## 六、常见问题
### 1、为什么连接的时候是三次握手，关闭的时候却是四次握手？
> 因为当Server端收到Client端的SYN连接请求报文后，可以直接发送SYN+ACK报文。其中ACK报文是用来应答的，SYN报文是用来同步的。但是关闭连接时，当Server端收到FIN报文时，很可能并不会立即关闭SOCKET，所以只能先回复一个ACK报文，告诉Client端，"你发的FIN报文我收到了"。只有等到我Server端所有的报文都发送完了，我才能发送FIN报文，因此不能一起发送。故需要四步握手。


## 七、参考连接
 - [http://blog.163.com/wangzhenbo85@126/blog/static/1013632822013423502833/?suggestedreading&wumii](http://blog.163.com/wangzhenbo85@126/blog/static/1013632822013423502833/?suggestedreading&wumii)
 - [https://www.cnblogs.com/zxh930508/p/5432700.html](https://www.cnblogs.com/zxh930508/p/5432700.html)