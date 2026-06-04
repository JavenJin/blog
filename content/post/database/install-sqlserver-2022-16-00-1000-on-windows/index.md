---
title: Install SQLServer 2022 (16.00.1000) on Windows
description: 在 Windows 上安装 SQLServer 2022 (16.00.1000)
date: '2024-01-22'
slug: install-sqlserver-2022-16-00-1000-on-windows
categories:
    - Database
tags:
    - Database
---

# Install SQLServer 2022 (16.00.1000) on Windows

## Go to the official website to download the SQLServer2022 installation package

Download the SQLServer 2022 installation package.

[https://www.microsoft.com/en-us/sql-server/sql-server-downloads](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).

![](images/image01.png)

## Open the installation package

![](images/image02.png)

## Select Download Media

![](images/image03.png)

## Choose to download the ISO file, Download Location, click Download

![](images/image04.png)

## Waiting for the download to complete

![](images/image05.png)

![](images/image06.png)

## Once the download is complete, right-click download image and select Mount

![](images/image07.png)

## Double-click the setup.exe programme in the pop-up page

![](images/image08.png)

## Waiting to enter the installation screen

![](images/image09.png)

## Click to Installation

![](images/image10.png)

## Choose New SQL Server standalone installation or add features to an existing installation

![](images/image11.png)

## Select the installation version Evaluation, Developer and click Next

![](images/image12.png)

## Choose to accept the terms of the licence and click Next

![](images/image13.png)

## Deselect Check for updates (checking for updates is not recommended, it is time consuming) and click Next

![](images/image14.png)

## Uncheck Azure Extension and click Next

![](images/image15.png)

## Function selection, it is recommended to select these two basic functions, change the instance root directory, click Next

![](images/image16.png)

## Instance configuration, here usually choose the default instance, click Next

![](images/image17.png)

## Service account configuration, here you can choose the SQL Server agent and engine account, usually keep the default and can be changed after the installation

![](images/image18.png)

## Sorting rules settings, generally keep the default, if you need to modify click Custom, select the specified sorting rules (Note: database migration and high availability to maintain the same sorting rules, sorting rules are not easy to modify after installation), click Next!

![](images/image19.png)

## Server Configuration. Select mixed mode, set sa password (sa is the super administrator of sql server), click add current user

![](images/image20.png)

## Data directory, here you can change the default location of the user database files, you can keep the default, it is recommended to create a separate directory for distribution

![](images/image21.png)

## TempDB (system temporary database, restart the database automatically updated), you can set the initial number of TempDB data files (recommended 4-8, do not exceed 8) and TempDB data file directory, it is recommended to allocate a separate disk and directory, you can keep the default, click Next!

![](images/image22.png)

## Click to install

![](images/image23.png)

## Waiting for installation to complete

![](images/image24.png)

## Click to close and the installation is complete

![](images/image25.png)