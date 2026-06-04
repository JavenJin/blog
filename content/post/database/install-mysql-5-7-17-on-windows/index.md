---
title: Install MySQL-5.7.17 on Windows
description: 在Windows上安装MySQL-5.7.17
date: '2021-05-29'
slug: install-mysql-5-7-17-on-windows
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

![](images/image01.png)

## Check the box I accept the license terms and click Next

![](images/image02.png)

## Check the Custom box and click Next

![](images/image03.png)

## Select the installation version x64 for 64-bit systems and x86 for 32-bit systems

![](images/image04.png)

## Then click on the right to select the following Advanced Options, to customize the path, I installed in the D disk root directory, and then OK, and then Next

![](images/image05.png)

## Continue to click Execute and wait for the installation

![](images/image06.png)

## Click Next after installation, continue to Next

![](images/image07.png)

## Select Server Dedicated

![](images/image08.png)

## Set the port number, generally not recommended to modify, the default 3306 can be, and then Next

![](images/image09.png)

## Enter the mysql password, and then Next

![](images/image10.png)

## Set the server name, which generally does not need to be changed either, and then Next

![](images/image11.png)

## No need to modify directly Next

![](images/image12.png)

## Click Execute to start the installation

![](images/image13.png)

## Click Finish

![](images/image14.png)

## Click Next

![](images/image15.png)

## Click Finish

![](images/image16.png)

## Open the my.ini file in the installation directory

![](images/image17.png)

## Change these two lines to innodb_flush_log_at_trx_commit=0 and innodb_buffer_pool_size=2G

![](images/image18.png)

![](images/image19.png)

## Save the changes and go to the bin folder in the installation directory

![](images/image20.png)

## Click on the address bar above and type cmd, then enter to open the command line in that directory

![](images/image21.png)

## Enter the command: "mysql -uroot -p", then enter the password to enter the mysql database

![](images/image22.png)

## Enter "status" and the following image will be displayed to indicate that the installation is complete

![](images/image23.png)