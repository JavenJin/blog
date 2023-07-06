---
title: MySQL Remote Access
description: MySQL远程访问
date: '2022-05-11'
categories:
    - Database
tags:
    - Database
---

# MySQL Remote Access

## Go to the bin directory in the MySQL installation directory (if you have configured environment variables, go directly to step 2)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MySQL%20Remote%20Access/mysql-remote-access-1.png)

## Type cmd in the address bar to open a command line window (if you have configured the environment variables directly Win+R type cmd to enter)

## Type the command and enter

```
mysql -uroot -p
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MySQL%20Remote%20Access/mysql-remote-access-2.png)

## Enter the command and enter, where password is the password of your msyql database

```
grant all privileges on *.* to 'root'@'%' identified by 'password';
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MySQL%20Remote%20Access/mysql-remote-access-3.png)

## Type the command and enter

```
flush privileges;
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MySQL%20Remote%20Access/mysql-remote-access-4.png)

## Close the window and finish

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MySQL%20Remote%20Access/mysql-remote-access-5.png)
