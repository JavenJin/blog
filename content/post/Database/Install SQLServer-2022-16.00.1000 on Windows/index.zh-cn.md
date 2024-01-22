---
title: 在 Windows 上安装 SQLServer 2022 (16.00.1000)
description: Install SQLServer 2022 (16.00.1000) on Windows
date: '2024-01-22'
categories:
    - Database
tags:
    - Database
---

# 在 Windows 上安装 SQLServer 2022 (16.00.1000)

## 前往官网下载SQLServer2022安装包

下载SQLServer2022安装包。

[https://www.microsoft.com/en-us/sql-server/sql-server-downloads](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-1.png)

## 打开安装包

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-2.png)

## 选择下载介质

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-3.png)

## 选择下载ISO文件，下载位置，点击下载

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-4.png)

## 等待下载完成

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-5.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-6.png)

## 下载完成之后，右键下载镜像，点击装载

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-7.png)

## 在弹出的页面中双击setup.exe程序

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-8.png)

## 等待进入安装界面

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-9.png)

## 点击安装

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-10.png)

## 选择全新SQL Server独立安装或向现有安装添加功能

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-11.png)

## 选择安装版本Evaluation（试用版），Developer（开发者版），点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-12.png)

## 选择接受许可条款，点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-13.png)

## 取消选择检查更新（这里不建议勾选，检查更新比较耗时），点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-14.png)

## 取消勾选Azure Extension，点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-15.png)

## 功能选择，建议选择这两个基本功能，更改实例根目录，点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-16.png)

## 实例配置，这里一般选择默认实例，点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-17.png)

## 服务账户配置，这里可以选择SQL Server代理和引擎的账户，一般保持默认并且安装好后还可以修改

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-18.png)

## 排序规则设置，一般保持默认，如需要修改点击自定义，选择指定排序规则（注意：数据库迁移和高可用搭建需保持排序规则一致，排序规则在安装后不易修改），点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-19.png)

## 服务器配置。选择混合模式，设置sa密码（sa是sql server的超级管理员），点击添加当前用户

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-20.png)

## 数据目录，这里可以更改用户数据库文件的默认位置，可以保持默认，建议单独建立目录进行分配

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-21.png)

## TempDB（系统临时数据库，重启数据库自动更新），可以设置TempDB数据文件初始数量（建议4-8个，不要超过8个）和TempDB数据文件目录，建议单独分配磁盘和目录，可以保持默认，点击下一步

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-22.png)

## 点击安装

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-23.png)

## 等待安装完成

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-24.png)

## 点击关闭，安装完成

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-25.png)