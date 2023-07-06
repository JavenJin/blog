---
title: Install Tomcat8 on Windows
description: 在Windows上安装Tomcat8
date: '2021-07-26'
categories:
    - Tools
tags:
    - Tools
---

# Install Tomcat8 on Windows

## Download the installation package

**Visit Tomcat official website [https://tomcat.apache.org/](https://tomcat.apache.org/)**

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20Tomcat8%20on%20Windows/install-tomcat8-1.png)

**Select the download version in the Download column on the left, the version selected here is Tomcat8, click into **

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20Tomcat8%20on%20Windows/install-tomcat8-2.png)

**Choose the corresponding version to download according to your system version, here choose the Windows 64-bit operating system version, as shown in the picture click download**

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20Tomcat8%20on%20Windows/install-tomcat8-3.png)

## Install Tomcat8 (the downloaded zip package is the installation-free version, you can use it directly after decompression)

**Unzip the downloaded file**

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20Tomcat8%20on%20Windows/install-tomcat8-4.png)

**Place the unpacked files on the D drive**

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20Tomcat8%20on%20Windows/install-tomcat8-5.png)

## Configure environment variables

**Right-click on properties on this computer and open settings**

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20Tomcat8%20on%20Windows/install-tomcat8-6.png)

**Click on Advanced System Settings to open System Properties**

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20Tomcat8%20on%20Windows/install-tomcat8-7.png)

**Click on environment variables to open environment variables**

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20Tomcat8%20on%20Windows/install-tomcat8-8.png)

**Select path and click edit to enter the edit path variable page**

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20Tomcat8%20on%20Windows/install-tomcat8-9.png)

**Click New, enter the directory of the bin folder under the installation directory of Tomcat8, click OK, OK, OK**

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20Tomcat8%20on%20Windows/install-tomcat8-10.png)

## Run the command

**Go to the bin folder in the Tomcat8 installation directory**

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20Tomcat8%20on%20Windows/install-tomcat8-11.png)

**Click on the address bar, type cmd and enter to open a command line window**

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20Tomcat8%20on%20Windows/install-tomcat8-12.png)

**Type service.bat install in the command line window and enter**

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20Tomcat8%20on%20Windows/install-tomcat8-13.png)

**The installation is successful if the picture is displayed**

## Test whether it is successful

**Double-click to run the Tomcat8w.exe file in the bin folder to open the startup window**

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20Tomcat8%20on%20Windows/install-tomcat8-14.png)

**Click Start to start Tomcat8**

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20Tomcat8%20on%20Windows/install-tomcat8-15.png)

**Open the browser, enter 127.0.0.1:8080 to access the following screen is a successful installation**

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Tools/Install%20Tomcat8%20on%20Windows/install-tomcat8-16.png)
