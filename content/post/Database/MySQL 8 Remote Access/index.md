---
title: MySQL 8 Remote Access
description: MySQL 8 远程访问
date: '2023-11-16'
categories:
    - Database
tags:
    - Database
---

# MySQL 8 Remote Access

## Go to the bin directory in the MySQL installation directory (if you have configured environment variables go directly to step 2)

## Type cmd in the address bar to open a command line window (if you have configured environment variables directly Win + R type cmd enter can be)

## Type the command and enter

```
mysql -uroot -p
```

## Type the command and enter, where password is the password for your msyql database

```
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%';
```

## Type the command and enter

```
FLUSH PRIVILEGES;
```

## Close the window and finish
