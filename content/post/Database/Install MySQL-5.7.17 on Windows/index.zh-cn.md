---
title: 在Windows上安装MySQL-5.7.17
description: Install MySQL-5.7.17 on Windows
date: '2021-05-29'
categories:
    - Database
tags:
    - Database
---

# 在Windows上安装MySQL-5.7.17

## 下载mysql安装包

下载mysql安装包。[mysql-5.7.17.msi](https://download.csdn.net/download/weixin_42718701/19201693).

或前往官网下载安装包。

## 打开安装包

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-1.png)

## 勾选I accept the license terms然后点击Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-2.png)

## 勾选Custom（自定义）然后点击Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-3.png)

## 选择安装版本64位系统选择x64，32位系统选择x86

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-4.png)

## 然后点击右边选择的下方Advanced Options，进行自定义路径，我装在了D盘根目录下，然后OK，然后Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-5.png)

## 继续点Execute，等待安装

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-6.png)

## 安装好了后点击Next，继续Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-7.png)

## 选择服务器专用

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-8.png)

## 设置端口号，一般不建议修改，默认3306即可，然后Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-9.png)

## 输入mysql密码，然后Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-10.png)

## 设置服务器名称，一般也不需要修改，然后Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-11.png)

## 不需要修改直接Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-12.png)

## 点击Execute，开始安装

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-13.png)

## 点击Finish

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-14.png)

## 点击Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-15.png)

## 点击Finish

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-16.png)

## 打开安装目录下的my.ini文件

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-17.png)

## 修改其中的这两行为innodb_flush_log_at_trx_commit=0和innodb_buffer_pool_size=2G

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-18.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-19.png)

## 修改完成后保存，进入到安装目录中的bin文件夹下

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-20.png)

## 点击上方地址栏输入cmd，然后回车，在该目录打开命令行

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-21.png)

## 输入命令："mysql -uroot -p"，然后输入密码，进入mysql数据库

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-22.png)

## 输入"status"，显示如下图即安装完毕

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-23.png)