---
title: MySQL 5.7 Remote Access
description: MySQL 5.7 远程访问
date: '2022-05-11'
categories:
    - Database
tags:
    - Database
---

# MySQL 5.7 远程访问

## 进入MySQL安装目录下的bin目录（如果配置过环境变量就直接到第二步）

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MySQL%205.7%20Remote%20Access/mysql-5.7-remote-access-1.png)

## 在地址栏输入cmd打开命令行窗口（如果配置过环境变量直接Win+R输入cmd回车即可）

## 输入命令并回车

```
mysql -uroot -p
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MySQL%205.7%20Remote%20Access/mysql-5.7-remote-access-2.png)

## 输入命令并回车，其中password是你msyql数据库的密码

```
grant all privileges on *.* to 'root'@'%' identified by 'password';
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MySQL%205.7%20Remote%20Access/mysql-5.7-remote-access-3.png)

## 输入命令并回车

```
flush privileges;
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MySQL%205.7%20Remote%20Access/mysql-5.7-remote-access-4.png)

## 关闭窗口，完成

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MySQL%205.7%20Remote%20Access/mysql-5.7-remote-access-5.png)
