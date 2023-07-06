---
title: Install MySQL-5.7.17 on Windows
description: 在Windows上安装MySQL-5.7.17
date: '2021-05-29'
categories:
    - Database
tags:
    - Database
---

# Install MySQL-5.7.17 on Windows

## Download the mysql installation package.

Download the mysql installation package: [mysql-5.7.17.msi](https://download.csdn.net/download/weixin_42718701/19201693).

Or go to the official website to download the installation package.

## Open the installation package

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-1.png)

## Check the box I accept the license terms and click Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-2.png)

## Check the Custom box and click Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-3.png)

## Select the installation version x64 for 64-bit systems and x86 for 32-bit systems

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-4.png)

## Then click on the right to select the following Advanced Options, to customize the path, I installed in the D disk root directory, and then OK, and then Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-5.png)

## Continue to click Execute and wait for the installation

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-6.png)

## Click Next after installation, continue to Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-7.png)

## Select Server Dedicated

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-8.png)

## Set the port number, generally not recommended to modify, the default 3306 can be, and then Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-9.png)

## Enter the mysql password, and then Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-10.png)

## Set the server name, which generally does not need to be changed either, and then Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-11.png)

## No need to modify directly Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-12.png)

## Click Execute to start the installation

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-13.png)

## Click Finish

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-14.png)

## Click Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-15.png)

## Click Finish

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-16.png)

## Open the my.ini file in the installation directory

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-17.png)

## Change these two lines to innodb_flush_log_at_trx_commit=0 and innodb_buffer_pool_size=2G

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-18.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-19.png)

## Save the changes and go to the bin folder in the installation directory

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-20.png)

## Click on the address bar above and type cmd, then enter to open the command line in that directory

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-21.png)

## Enter the command: "mysql -uroot -p", then enter the password to enter the mysql database

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-22.png)

## Enter "status" and the following image will be displayed to indicate that the installation is complete

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7.17%20on%20Windows/install-mysql-5-7-17-23.png)