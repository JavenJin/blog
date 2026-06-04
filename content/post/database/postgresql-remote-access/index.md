---
title: PostgreSQL Remote Access
description: PostgreSQL远程访问
date: '2022-05-11'
categories:
    - Database
tags:
    - Database
---

# PostgreSQL Remote Access

## Open the data\pg_hba.conf file in the PostgreSQL installation directory

![](images/image01.png)

## Add the following line

```
host	all		        all		        0.0.0.0/0		        scram-sha-256
```

![](images/image02.png)

## Save to exit, done

![](images/image03.png)
