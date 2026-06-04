---
title: Install Oracle-12c-R2 on Windows
description: 在Windows上安装Oracle-12c-R2
date: '2023-12-12'
categories:
    - Database
tags:
    - Database
---

# Install Oracle-12c-R2 on Windows

Oracle Download Address:
[https://edelivery.oracle.com/osdc/faces/SoftwareDelivery](https://edelivery.oracle.com/osdc/faces/SoftwareDelivery)

## Log in to your Oracle account

Open the Oracle download address connection, enter the Oracle account password login (if you do not have an account, please register an account first)

![](images/image01.png)

## Download the installation package

1. Enter the following text in the search box to search for installers

```
Oracle Database 12c Enterprise Edition
```

2. Select a version of the installation package as follows

```
Oracle Database 12c Personal Edition 12.1.0.2.0
```

![](images/image02.png)

3. Click on View Items in the upper right

![](images/image03.png)

4. Select the corresponding installation environment and language, confirm and click Continue.

![](images/image04.png)

5. Select Agree and click Continue

![](images/image05.png)

6. Click to Download

![](images/image06.png)

7. Open the downloaded downloader

![](images/image07.png)

8. Select the download path and click Next

![](images/image08.png)

9. Waiting for the download to complete

![](images/image09.png)

10. Click on Open Destination when the download is complete

![](images/image10.png)

11. Unzip the two downloaded zip archives (both separately, in the same directory)

![](images/image11.png)

## Installing Oracle

1. Open the directory you just unzipped and double-click to run setup

![](images/image12.png)

2. No need to enter Email and no need for support, just tap Next and click Yes!

![](images/image13.png)

3. Select Create and configure a database and click Next.

![](images/image14.png)

4. Select the Desktop class and click Next.

![](images/image15.png)

5. Select Create New Windows User, enter your username and password and click Next.

![](images/image16.png)

6. Set the installation path, you can change the Global database name, enter the password, and other configuration items and click Next.

![](images/image17.png)

7. Wait for the installer to check the installation environment

![](images/image18.png)

8. Click Install

![](images/image19.png)

9. Waiting for installation

![](images/image20.png)

![](images/image21.png)

![](images/image22.png)

10. Click OK when the installation is complete (you can also click Password Management to configure passwords for other users).

![](images/image23.png)

## Verify that the installation was successful

1. The installation program will automatically install SQL Plus, open SQL Plus

![](images/image24.png)

2. Enter the system username SYSTEM and the password as you configured it yourself

![](images/image25.png)

3. Enter the following SQL to query the installed version

```sql
select * from product_component_version;
```

![](images/image26.png)