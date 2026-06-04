---
title: 在Windows上安装PostgreSQL 16.1
description: Install PostgreSQL 16.1 on Windows
date: '2023-11-15'
categories:
    - Database
tags:
    - Database
---

# 在Windows上安装PostgreSQL 16.1

## 前往官网下载PostgreSQL安装包

下载PostgreSQL安装包。

[https://www.enterprisedb.com/downloads/postgres-postgresql-downloads](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads).

![](images/image01.png)

## 打开安装包

![](images/image02.png)

## 点击Next

![](images/image03.png)

## 修改安装目录然后点击Next

![](images/image04.png)

## 保持默认选项，点击Next

![](images/image05.png)

## 设置数据目录，点击Next

![](images/image06.png)

## 设置密码，点击Next

![](images/image07.png)

## 设置数据库端口号（默认5432），点击Next

![](images/image08.png)

## 设置语言，点击Next

![](images/image09.png)

## 后面一直点Next即可

![](images/image10.png)

## 等待安装完毕

![](images/image11.png)

## 取消勾选Stack Builder，点击Finish

![](images/image12.png)

## 至此，PostgreSQL安装完毕

## PostgresSQL安装携带了pgAdmin软件，可以用来管理PostgreSQL数据库，打开pgAdmin

![](images/image13.png)

## 点击左上角的Server

![](images/image14.png)

## 输入设置的密码，点击OK

![](images/image15.png)

## 如下界面即表示安装成功

![](images/image16.png)

## 也可以使用第三方数据库连接器进行连接测试，PostgreSQL的用户名为postgres