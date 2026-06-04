---
title: MySQL 5.7 远程访问
description: MySQL 5.7 Remote Access
date: '2022-05-11'
slug: mysql-5-7-remote-access
categories:
    - Database
tags:
    - Database
---

# MySQL 5.7 远程访问

## 进入MySQL安装目录下的bin目录（如果配置过环境变量就直接到第二步）

![](images/image01.png)

## 在地址栏输入cmd打开命令行窗口（如果配置过环境变量直接Win+R输入cmd回车即可）

## 输入命令并回车

```
mysql -uroot -p
```

![](images/image02.png)

## 输入命令并回车，其中password是你msyql数据库的密码

```
grant all privileges on *.* to 'root'@'%' identified by 'password';
```

![](images/image03.png)

## 输入命令并回车

```
flush privileges;
```

![](images/image04.png)

## 关闭窗口，完成

![](images/image05.png)
