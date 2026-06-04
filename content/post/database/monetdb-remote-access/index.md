---
title: MonetDB Remote Access
description: MonetDB远程访问
date: '2022-05-11'
slug: monetdb-remote-access
categories:
    - Database
tags:
    - Database
---

# MonetDB Remote Access

## First of all, we should know that the normal way to start MonetDB is to run the M5server.bat file directly from the installation directory

![](images/image01.png)

## After starting up, the following picture, at this time directly using another computer's DBeaver connection will prompt that the connection is rejected

![](images/image02.png)

![](images/image03.png)

## Edit the M5server.bat file in the installation directory and add the --set "mapi_listenaddr=all" parameter to the start the real server command below

```
--set "mapi_listenaddr=all"
```

![](images/image04.png)

## Save the file and re-run M5server.bat

![](images/image05.png)

## Finish

![](images/image06.png)

## References

[https://www.monetdb.org/documentation-Jan2022/admin-guide/manpages/mserver5/](https://www.monetdb.org/documentation-Jan2022/admin-guide/manpages/mserver5/)