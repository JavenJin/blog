---
title: MonetDB远程访问
description: MonetDB Remote Access
date: '2022-05-11'
categories:
    - Database
tags:
    - Database
---

# MonetDB远程访问

## 首先我们应该知道正常启动MonetDB是直接运行安装目录下的M5server.bat文件

![](images/image01.png)

## 启动后如下图，这时候直接使用另一台电脑的DBeaver连接会提示连接被拒绝

![](images/image02.png)

![](images/image03.png)

## 编辑安装目录下的M5server.bat文件，给下面start the real server命令后面加上--set "mapi_listenaddr=all"参数

```
--set "mapi_listenaddr=all"
```

![](images/image04.png)

## 保存文件重新运行M5server.bat

![](images/image05.png)

## 完成

![](images/image06.png)

## 参考资料

[https://www.monetdb.org/documentation-Jan2022/admin-guide/manpages/mserver5/](https://www.monetdb.org/documentation-Jan2022/admin-guide/manpages/mserver5/)