---
title: PostgreSQL远程访问
description: PostgreSQL Remote Access
date: '2022-05-11'
categories:
    - Database
tags:
    - Database
---

# PostgreSQL远程访问

## 打开PostgreSQL安装目录下data\pg_hba.conf文件

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/PostgreSQL%20Remote%20Access/postgresql-remote-access-1.png)

## 添加如下行

```
host	all		        all		        0.0.0.0/0		        scram-sha-256
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/PostgreSQL%20Remote%20Access/postgresql-remote-access-2.png)

## 保存退出，完成

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/PostgreSQL%20Remote%20Access/postgresql-remote-access-3.png)
