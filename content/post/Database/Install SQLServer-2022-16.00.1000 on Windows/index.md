---
title: Install SQLServer 2022 (16.00.1000) on Windows
description: 在 Windows 上安装 SQLServer 2022 (16.00.1000)
date: '2024-01-22'
categories:
    - Database
tags:
    - Database
---

# Install SQLServer 2022 (16.00.1000) on Windows

## Go to the official website to download the SQLServer2022 installation package

Download the SQLServer 2022 installation package.

[https://www.microsoft.com/en-us/sql-server/sql-server-downloads](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-1.png)

## Open the installation package

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-2.png)

## Select Download Media

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-3.png)

## Choose to download the ISO file, Download Location, click Download

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-4.png)

## Waiting for the download to complete

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-5.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-6.png)

## Once the download is complete, right-click download image and select Mount

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-7.png)

## Double-click the setup.exe programme in the pop-up page

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-8.png)

## Waiting to enter the installation screen

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-9.png)

## Click to Installation

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-10.png)

## Choose New SQL Server standalone installation or add features to an existing installation

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-11.png)

## Select the installation version Evaluation, Developer and click Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-12.png)

## Choose to accept the terms of the licence and click Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-13.png)

## Deselect Check for updates (checking for updates is not recommended, it is time consuming) and click Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-14.png)

## Uncheck Azure Extension and click Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-15.png)

## Function selection, it is recommended to select these two basic functions, change the instance root directory, click Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-16.png)

## Instance configuration, here usually choose the default instance, click Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-17.png)

## Service account configuration, here you can choose the SQL Server agent and engine account, usually keep the default and can be changed after the installation

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-18.png)

## Sorting rules settings, generally keep the default, if you need to modify click Custom, select the specified sorting rules (Note: database migration and high availability to maintain the same sorting rules, sorting rules are not easy to modify after installation), click Next!

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-19.png)

## Server Configuration. Select mixed mode, set sa password (sa is the super administrator of sql server), click add current user

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-20.png)

## Data directory, here you can change the default location of the user database files, you can keep the default, it is recommended to create a separate directory for distribution

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-21.png)

## TempDB (system temporary database, restart the database automatically updated), you can set the initial number of TempDB data files (recommended 4-8, do not exceed 8) and TempDB data file directory, it is recommended to allocate a separate disk and directory, you can keep the default, click Next!

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-22.png)

## Click to install

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-23.png)

## Waiting for installation to complete

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-24.png)

## Click to close and the installation is complete

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20SQLServer-2022-16.00.1000%20on%20Windows/Install-SQLServer-2022-16.00.1000-on-Windows-25.png)