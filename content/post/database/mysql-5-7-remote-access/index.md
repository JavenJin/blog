---
title: MySQL 5.7 Remote Access
description: MySQL 5.7 远程访问
date: '2022-05-11'
categories:
    - Database
tags:
    - Database
---

# MySQL 5.7 Remote Access

## Go to the bin directory in the MySQL installation directory (if you have configured environment variables, go directly to step 2)

![](images/image01.png)

## Type cmd in the address bar to open a command line window (if you have configured the environment variables directly Win+R type cmd to enter)

## Type the command and enter

```
mysql -uroot -p
```

![](images/image02.png)

## Enter the command and enter, where password is the password of your msyql database

```
grant all privileges on *.* to 'root'@'%' identified by 'password';
```

![](images/image03.png)

## Type the command and enter

```
flush privileges;
```

![](images/image04.png)

## Close the window and finish

![](images/image05.png)
