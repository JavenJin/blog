---
title: MySQL 8 远程访问
description: MySQL 8 Remote Access
date: '2023-11-16'
categories:
    - Database
tags:
    - Database
---

# MySQL 8 远程访问

## 进入MySQL安装目录下的bin目录（如果配置过环境变量就直接到第二步）

## 在地址栏输入cmd打开命令行窗口（如果配置过环境变量直接Win+R输入cmd回车即可）

## 输入命令并回车

```
mysql -uroot -p
```

## 输入命令并回车，其中password是你msyql数据库的密码

```
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%';
```

## 输入命令并回车

```
FLUSH PRIVILEGES;
```

## 关闭窗口，完成
