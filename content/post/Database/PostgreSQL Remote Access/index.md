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

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/PostgreSQL%20Remote%20Access/postgresql-remote-access-1.png)

## Add the following line

```
host	all		        all		        0.0.0.0/0		        scram-sha-256
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/PostgreSQL%20Remote%20Access/postgresql-remote-access-2.png)

## Save to exit, done

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/PostgreSQL%20Remote%20Access/postgresql-remote-access-3.png)
