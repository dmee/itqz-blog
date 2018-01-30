---
title: MongoDB用户权限管理
date: 2018-01-30 23:18:10
tags:
    - MongoDB
category: MongoDB
---
## MongoDB 用户权限管理手册
[https://docs.mongodb.com/manual/reference/method/js-user-management/](https://docs.mongodb.com/manual/reference/method/js-user-management/)


## 创建用户
```javascript
db.createUser(user, writeConcern);

db.createUser({ 
    user: "<name>",
    pwd: "<cleartext password>",
    customData: { <any information> },
    roles: [
        { role: "<role>", db: "<database>" } | "<role>",
        ...
    ]
});
```
### 参数详解

#### user（需要创建的用户信息）
  - user:新建用户名
  - pwd:新建用户密码
  - customData:存放一些用户相关的自定义数据
  - roles:数组类型，配置用户的权限

**[常用权限](https://docs.mongodb.com/manual/reference/built-in-roles/)**

|   角色类型    |   权限级别    |
|   ---      |   ---         |
| 普通用户角色  |   read、readWrite    |
| 数据库管理员角色  |   dbAdmin、dbOwner、userAdmin    |
|集群管理员角色 |   clusterAdmin、clusterManager、clusterMonitor、hostManager|
|数据库备份与恢复角色|  backup、restore |
| 所有数据库角色 |  readAnyDatabase、readWriteAnyDatabase、userAdminAnyDatabase、dbAdminAnyDatabase|
| 超级用户角色 | root |
| 核心角色 | __system |

#### writeConcern（对写操作时的异常处理机制）

下面我们列一下WriteConcern的几种抛出异常的级别参数：

 - WriteConcern.NONE:没有异常抛出
 - WriteConcern.NORMAL:仅抛出网络错误异常，没有服务器错误异常
 - WriteConcern.SAFE:抛出网络错误异常、服务器错误异常；并等待服务器完成写操作。
 - WriteConcern.MAJORITY: 抛出网络错误异常、服务器错误异常；并等待一个主服务器完成写操作。
 - WriteConcern.FSYNC_SAFE: 抛出网络错误异常、服务器错误异常；写操作等待服务器将数据刷新到磁盘。
 - WriteConcern.JOURNAL_SAFE:抛出网络错误异常、服务器错误异常；写操作等待服务器提交到磁盘的日志文件。
 - WriteConcern.REPLICAS_SAFE:抛出网络错误异常、服务器错误异常；等待至少2台服务器完成写操作。

### 代码案例
```javascript
db.createUser({ 
    user: "root",
    pwd: "123456",
    customData: {
        create_date: '2016-09-03'
    },
    roles: [
        {
            role: "read", 
            db: "db_test_one" 
        },{
            role: "userAdmin", 
            db: "db_test_two" 
        }
    ]
});
```


## 查找指定用户

### 方法一

```javascript
db.system.users.find()
```
### 方法二

```javascript
db.getUser(username, args)
```

### 参数详解

#### username:要查找的用户名
#### args（查询用户时的附加参数）
 - showPrivileges:布尔值，默认为false。贤惠用户的权限
 - showCredentials:布尔值，默认为false。显示用户的password hash

## 查找全部用户

```javascript
db.getUsers()
```

## 修改用户

```javascript
db.updateUser(username, update, writeConcern)

db.updateUser(
   "<username>",
   {
     customData : { <any information> },
     roles : [
               { role: "<role>", db: "<database>" } | "<role>",
               ...
             ],
     pwd: "<cleartext password>"
    },
    writeConcern: { <write concern> }
)
```
### 参数详解

#### username:要查找的用户名
#### update:更新后的数据
 - customData:设置用户的自定义数据
 - roles:数组类型，设置用户的角色
 - pwd:字符串类型，设置修改的用户名

#### writeConcern:对写操作时的异常处理机制，详情参考***db.createUser***

### 代码案例
```javascript
db.updateUser(
    "root",{
        customData:{
            create_time:"2016-09-03",
            update_time:"2016-09-04"
        },
        pwd:"123456"
    }
)
```
## 修改用户密码
```javascript
db.changeUserPassword(username, password)
```

### 参数详解

#### username:要修改的用户名
#### password:要修改的密码
#### mechanism:密码验证机制
 - SCRAM-SHA-1
 - MONGODB-CR

#### digestPassword:布尔值，是否为加密密码


## 删除用户
### 方式一

```javascript
db.system.users.remove(query)
```

### 方式二
```javascript
db.removeUser(username)
```

### 方式三
```javascript
db.dropUser(username, writeConcern) //从当前数据库删除用户

db.dropAllUsers(writeConcern) //从当前数据库删除所有用户
```

## 用户绑定角色
```javascript
db.grantRolesToUser( "<username>", [ <roles> ], { <writeConcern> } )
```


## 用户角色解绑

```javascript
db.revokeRolesFromUser( "<username>", [ <roles> ], { <writeConcern> } )
```

## 用户Shell登录权限
```javascript
db.auth( <username>, <password> )

db.auth( {
   user: <username>,
   pwd: <password>,
   mechanism: <authentication mechanism>,
   digestPassword: <boolean>
} )
```



