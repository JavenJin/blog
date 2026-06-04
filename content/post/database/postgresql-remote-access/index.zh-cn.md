---
title: PostgreSQL远程访问
description: PostgreSQL Remote Access
date: '2022-05-11'
slug: postgresql-remote-access
categories:
    - Database
tags:
    - Database
---

# PostgreSQL远程访问

## 打开PostgreSQL安装目录下data\pg_hba.conf文件

![](images/image01.png)

## 添加如下行

```
host	all		        all		        0.0.0.0/0		        scram-sha-256
```

![](images/image02.png)

## 保存退出，完成

![](images/image03.png)
