---
title: Git 操作文档
tags: 
    - Git
category: Git
date: 2018-01-26 17:04:43
---

## 分支操作

#### 查看本地分支
> git branch

#### 查看远端分支
> git branch -a

#### 检出分支
> git checkout branchName

#### 检出文件并覆盖
> git checkout -- fileName

#### 抓取远端分支并清理已删除分支
> git remote show origin
> git remote prune origin