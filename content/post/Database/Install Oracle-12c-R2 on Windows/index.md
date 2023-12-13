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

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-1.png)

## Download the installation package

1. Enter the following text in the search box to search for installers

```
Oracle Database 12c Enterprise Edition
```

2. Select a version of the installation package as follows

```
Oracle Database 12c Personal Edition 12.1.0.2.0
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-2.png)

3. Click on View Items in the upper right

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-3.png)

4. Select the corresponding installation environment and language, confirm and click Continue.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-4.png)

5. Select Agree and click Continue

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-5.png)

6. Click to Download

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-6.png)

7. Open the downloaded downloader

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-7.png)

8. Select the download path and click Next

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-8.png)

9. Waiting for the download to complete

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-9.png)

10. Click on Open Destination when the download is complete

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-10.png)

11. Unzip the two downloaded zip archives (both separately, in the same directory)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-11.png)

## Installing Oracle

1. Open the directory you just unzipped and double-click to run setup

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-12.png)

2. No need to enter Email and no need for support, just tap Next and click Yes!

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-13.png)

3. Select Create and configure a database and click Next.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-14.png)

4. Select the Desktop class and click Next.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-15.png)

5. Select Create New Windows User, enter your username and password and click Next.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-16.png)

6. Set the installation path, you can change the Global database name, enter the password, and other configuration items and click Next.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-17.png)

7. Wait for the installer to check the installation environment

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-18.png)

8. Click Install

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-19.png)

9. Waiting for installation

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-20.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-21.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-22.png)

10. Click OK when the installation is complete (you can also click Password Management to configure passwords for other users).

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-23.png)

## Verify that the installation was successful

1. The installation program will automatically install SQL Plus, open SQL Plus

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-24.png)

2. Enter the system username SYSTEM and the password as you configured it yourself

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-25.png)

3. Enter the following SQL to query the installed version

```sql
select * from product_component_version;
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20Oracle-12c-R2%20on%20Windows/Install-Oracle-12c-R2-on-Windows-26.png)