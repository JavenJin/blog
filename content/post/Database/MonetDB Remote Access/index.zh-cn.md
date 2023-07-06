---
title: MonetDB Remote Access
description: MonetDB远程访问
date: '2022-05-11'
categories:
    - Database
tags:
    - Database
---

# MonetDB远程访问

## 首先我们应该知道正常启动MonetDB是直接运行安装目录下的M5server.bat文件

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MonetDB%20Remote%20Access/monetdb-remote-access-1.png)

## 启动后如下图，这时候直接使用另一台电脑的DBeaver连接会提示连接被拒绝

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MonetDB%20Remote%20Access/monetdb-remote-access-2.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MonetDB%20Remote%20Access/monetdb-remote-access-3.png)

## 编辑安装目录下的M5server.bat文件，给下面start the real server命令后面加上--set "mapi_listenaddr=all"参数

```
--set "mapi_listenaddr=all"
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MonetDB%20Remote%20Access/monetdb-remote-access-4.png)

## 保存文件重新运行M5server.bat

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MonetDB%20Remote%20Access/monetdb-remote-access-5.png)

## 完成

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MonetDB%20Remote%20Access/monetdb-remote-access-6.png)

## 参考资料

[https://www.monetdb.org/documentation-Jan2022/admin-guide/manpages/mserver5/](https://www.monetdb.org/documentation-Jan2022/admin-guide/manpages/mserver5/)