---
title: 在Windows上安装Oracle-12c-R2
description: Install Oracle-12c-R2 on Windows
date: '2023-12-12'
categories:
    - Database
tags:
    - Database
---

# 在Windows上安装Oracle-12c-R2

Oracle下载地址：
[https://edelivery.oracle.com/osdc/faces/SoftwareDelivery](https://edelivery.oracle.com/osdc/faces/SoftwareDelivery)

## 登录Oracle账号

打开Oracle下载地址连接，输入Oracle账号密码登录（如果没有账号请先注册账号）

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-1.png)

## 下载安装包

1. 在搜索框输入如下文本，搜索安装包

```
Oracle Database 12c Enterprise Edition
```

2. 选择版本如下的安装包

```
Oracle Database 12c Personal Edition 12.1.0.2.0
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-2.png)

3. 点击右上方的View Items

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-3.png)

4. 选择对应的安装环境及语言，确认后点击Continue

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-4.png)

5. 选择同意并点击Continue

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-5.png)

6. 点击Download

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-6.png)

7. 打开下载下来的下载器

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-7.png)

8. 选择下载路径点击Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-8.png)

9. 等待下载完成

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-9.png)

10. 下载完成后点击Open Destination

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-10.png)

11. 解压下载下来的两个压缩包（两个分别都要解压，解压在同一目录下）

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-11.png)

## 安装Oracle

1. 打开刚才解压的目录，双击运行setup

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-12.png)

2. 不需要输入Email以及不需要支持，直接点Next，并点击Yes

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-13.png)

3. 选择Create and configure a database，并点击Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-14.png)

4. 选择Desktop class，并点击Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-15.png)

5. 选择Create New Windows User，输入用户名密码并点击Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-16.png)

6. 设置安装路径，可以修改Global database name，输入密码，以及其他配置项后点击Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-17.png)

7. 等待安装程序检查安装环境

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-18.png)

8. 点击Install

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-19.png)

9. 等待安装

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-20.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-21.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-22.png)

10. 安装完成后点击OK（也可以点击Password Management去配置其他用户的密码）

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-23.png)

## 验证安装是否成功

1. 安装程序会自动安装SQL Plus，打开SQL Plus

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-24.png)

2. 输入系统用户名SYSTEM，密码为你自己配置的密码

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-25.png)

3. 输入以下SQL，查询安装版本

```sql
select * from product_component_version;
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install%20Oracle-12c-R2%20on%20Windows-26.png)