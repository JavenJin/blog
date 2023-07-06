---
title: Install MySQL-5.7 on CentOS7
description: 在CentOS7上安装MySQL-5.7
date: '2021-08-11'
categories:
    - Database
tags:
    - Database
---

# Install MySQL-5.7 on CentOS7

At that time, the installation of mysql5.7 encountered many problems, online solutions are not right, record down their own installation of successful installation steps and notes

## Install mysql 5.7

### Update yum local cache

```bash
yum clean cache
yum makecache
```

### Check if mysql is installed on the system

```bash
yum list installed | grep mysql
```

### Uninstall mysql and its dependencies that come with the system (to prevent conflicts)

```bash
yum -y remove mysql-libs.x86_64
```

### Install wget

```bash
yum install wget -y
```

### Add rpm sources to centos and select the newer ones

```bash
wget dev.mysql.com/get/mysql-community-release-el6-5.noarch.rpm
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-1.png)

### Install the downloaded rpm file

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-2.png)

### Go to the directory /etc/yum.repos.d/ and these two files will be added

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-3.png)

### Modify the mysql-community.repo file

```bash
vi mysql-community.repo
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-4.png)

### Install mysql using yum

```bash
yum install mysql-community-server -y
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-5.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-6.png)

### Check the version of mysql to make sure it's installed successfully

```bash
mysql -V
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-7.png)

### Start mysql service

```bash
service mysqld start
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-8.png)

### Set mysql to start on boot

```bash
chkconfig mysqld on
```

### From the mysqld.log file, view the mysql temporary password

```bash
grep "password" /var/log/mysqld.log
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-9.png)

### Copy the temporary password above and login to mysql

```bash
mysql -uroot -p[Temporary password]
```

- If there are special characters in the temporary password, you need to add \\\\ escape, otherwise it will prompt the character exception
- Do not have spaces after -u and -p, or you will be prompted with a password error

### Change the password authentication policy (do not change it, the modified password may not pass), and then change the root user password

```sql
set global validate_password_policy=0;
set global validate_password_length=4;
alter user 'root'@'localhost' identified by '123456';
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-10.png)

- After successfully changing your password, type quit to log out, and then log back in with your new password.

### Set the database user to be accessible under all ip's, the following example with the root user (enter this command in mysql)

```sql
grant all privileges on *.* to 'root'@'%' identified by '123456' with grant option;
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-11.png)

- where root is the user, % indicates all privileges, and the password is 123456

### Refresh mysql's system permission-related tables (enter this command in mysql)

```sql
flush privileges;
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-12.png)

### Use quit or exit to quit mysql and restart mysql service

```bash
service mysqld restart
```

## Turn on the firewall

The linux firewall is not opened on port 3306 by default, you need to open it manually so that the local client can connect to the mysql service on linux.

### Check if port 3306 is open

```bash
firewall-cmd --query-port=3306/tcp
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-13.png)

- yes, means on; no means not on

### On the firewall, add the port 3306 that needs to be opened

```bash
firewall-cmd --add-port=3306/tcp --permanent
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-14.png)

### Reload the added port

```bash
firewall-cmd --reload
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-15.png)

### Query again whether port 3306 is open, and confirm that it is open

```bash
firewall-cmd --query-port=3306/tcp
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-16.png)

## Uninstall mysql on linux

If the installation fails and you want to reinstall it, you need to remove all mysql related ones.

### Check the installed mysql components

```bash
rpm -qa | grep -i mysql
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-17.png)

### Delete the queried files one by one

```bash
yum remove mysql-community-libs-compat-5.7.35-1.el7.x86_64
yum remove mysql-community-release-el6-5.noarch
yum remove mysql-community-common-5.7.35-1.el7.x86_64
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-18.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/Install%20MySQL-5.7%20on%20CentOS7/install-mysql-5-7-19.png)

### Delete mysql related files

```bash
yum remove mysql mysql-server mysql-libs mysql-server
rm -rf /var/lib/mysq
rm /etc/my.cnf
rm –rf /usr/lib64/mysql
rm -rf /etc/yum.repos.d/mysql*
rm -rf mysql-community-release-el6-5.noarch.rpm
```

### Find residual directories, then use the rm command to delete them one by one

```bash
whereis mysql
```