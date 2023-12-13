---
title: Install DM8 on Windows
description: 在Windows上安装DM8
date: '2023-12-13'
categories:
    - Database
tags:
    - Database
---

# Install DM8 on Windows

## Download the installation image

1. Visit the official website to download and install the mirror

[https://www.dameng.com/](https://www.dameng.com/)

2. Unzip the package

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-1.png)

## Installing the DM8

1. Run the installation program

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-2.png)

2. Start setup.exe in the directory

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-3.png)

3. Language and Time Zone Selection

Select the appropriate language and time zone according to your system configuration and click the OK button to continue the installation.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-4.png)

4. Welcome Page

Click the Next button to continue the installation.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-5.png)

5. License Agreement

Select Accept Agreement and click Next to continue the installation.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-6.png)

6. Verify the Key file

Click Next directly to continue the installation

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-7.png)

7. Selecting Installation Components

The DM installer provides four installation methods: "Typical Installation", "Server Installation", "Client Installation" and "Custom Installation". The DM installer provides four installation methods: "Typical Installation", "Server Installation", "Client Installation" and "Customized Installation". As shown in the figure below:

Typical installation includes: server, client, driver, user manual, database service.

Server installation includes: server, driver, user manual, database service.

Client installation includes: client, driver, user manual.

Customized installation includes: user check the components according to the requirements, it can be any combination of server, client, driver, user manual, database service.

Click Next to continue the installation.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-8.png)

8. Select installation directory

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-9.png)

9. Pre-installation Summary

Displays information about the upcoming installation, such as product name, version information, installation type, installation directory, free space, free memory, etc. Users check for accuracy and then click the Install button to proceed with the installation of DM.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-10.png)

10. Installation Process

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-11.png)

Wait for the installation to complete.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-12.png)

## Initializing the database

1. Initializing the database

After the installation is complete, you can click Init to initialize the database.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-13.png)

2. Selecting the Operation Method

Select Create Database Instance and click Start.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-14.png)

3. Creating database templates

The system provides three sets of database templates for users to choose from: General Purpose, On-line Analytical Processing and On-line Transaction Processing.

Select Common and click Next to continue.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-15.png)

4. Selecting the database directory

Set the database directory and click Next to continue.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-16.png)

5. Input database identification

Users can enter parameters such as database name, instance name, port number, etc.

Click Next to continue.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-17.png)

6. Database File Location

The user can determine the location of the database control, database log, and other files by selecting or typing them, and can add or delete files using the function buttons on the right.

Click Next to continue.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-18.png)

7. Database initialization parameters

Users can enter database related parameters, such as cluster size, page size, log file size, select character set, whether it is case sensitive or not.

Click Next to continue.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-19.png)

8. Password Management

Users can enter the password of SYSDBA, SYSAUDITOR to change the default password, if the installation version is the security version, it will add the password change of SYSSSO user.

Click Next to continue.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-20.png)

9. Choosing to Create a Sample Library

Users can choose whether to create a sample library BOOKSHOP or DMHR.

Click Next to continue.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-21.png)

10. Creating a Database Summary

Before installing the database, the relevant parameters set by the user through the database configuration tool will be displayed.

Click Finish to continue.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-22.png)

11. Install the initialization database

Wait for the installation to complete.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-23.png)

After the installation is complete, a pop-up will appear with database related parameters and file locations.

Click Finish to finish initializing the database.

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20DM8%20on%20Windows/Install-DM8-on-Windows-24.png)