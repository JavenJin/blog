---
title: MonetDB Remote Access
description: MonetDB远程访问
date: '2022-05-11'
categories:
    - Database
tags:
    - Database
---

# MonetDB Remote Access

## First of all, we should know that the normal way to start MonetDB is to run the M5server.bat file directly from the installation directory

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MonetDB%20Remote%20Access/monetdb-remote-access-1.png)

## After starting up, the following picture, at this time directly using another computer's DBeaver connection will prompt that the connection is rejected

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MonetDB%20Remote%20Access/monetdb-remote-access-2.png)

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MonetDB%20Remote%20Access/monetdb-remote-access-3.png)

## Edit the M5server.bat file in the installation directory and add the --set "mapi_listenaddr=all" parameter to the start the real server command below

```
--set "mapi_listenaddr=all"
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MonetDB%20Remote%20Access/monetdb-remote-access-4.png)

## Save the file and re-run M5server.bat

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MonetDB%20Remote%20Access/monetdb-remote-access-5.png)

## Finish

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/MonetDB%20Remote%20Access/monetdb-remote-access-6.png)

## References

[https://www.monetdb.org/documentation-Jan2022/admin-guide/manpages/mserver5/](https://www.monetdb.org/documentation-Jan2022/admin-guide/manpages/mserver5/)