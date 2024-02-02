---
title: Snowflake 中的 SHOW TABLES
description: SHOW TABLES in Snowflake
date: '2024-02-02'
categories:
    - Database
tags:
    - Database
---

# Snowflake 中的 SHOW TABLES

## 遇到的问题

在Snowflake中执行下面的SQL可以查询数据库中包含的表。

```sql
SHOW TABLES;
```

当我的数据库结构如下：

```
Snowflake Schema Test(database)
    JAVEN(schema)
        TestTable(table)
        TestTable1(table)
    PUBLIC(schema)
        TestTable(table)
        TestTable1(table)
        TestTable2(table)
```

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/SHOW%20TABLES%20in%20Snowflake/SHOW-TABLES-in-Snowflake-1.png)

此时，执行SHOW TABLES的结果如下：

|**created_on**|**name**|**database_name**|**schema_name**|**kind**|**owner**|
|:--|--|--|--|--|--|
|2024-02-01 23:30:24.534 -0800|TestTable|Snowflake Schema Test|JAVEN|TABLE|ACCOUNTADMIN|
|2024-02-01 23:30:30.178 -0800|TestTable1|Snowflake Schema Test|JAVEN|TABLE|ACCOUNTADMIN|
|2024-02-01 23:30:36.126 -0800|TestTable2|Snowflake Schema Test|PUBLIC|TABLE|ACCOUNTADMIN|

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/SHOW%20TABLES%20in%20Snowflake/SHOW-TABLES-in-Snowflake-2.png)

很明显，在数据库中包含5张表，但是查询出来仅剩下3张表。

## 问题原因

我们猜测可能是因为不同的Schema下有重名的表，Snowflake进行了去重。但是这是不对的，官方对此的解释如下：

> In the output, results are sorted by database name, schema name, and then table name. This means results for a database can contain tables from multiple schemas and might break pagination. In order for pagination to work as expected, **you must execute the SHOW TABLES command for a single schema**. You can use the IN SCHEMA \<schema_name\> parameter to the SHOW TABLES command. Alternatively, you can use the schema in the current context by executing a USE SCHEMA command before executing a SHOW TABLES command.

> References: [https://docs.snowflake.com/en/sql-reference/sql/show-tables#usage-notes](https://docs.snowflake.com/en/sql-reference/sql/show-tables#usage-notes)

意思是仅支持针对一个Schema来执行该SQL。

## 解决方案

当我们的业务必须需要一条SQL查询该数据库下的所有表的时候，直接使用SHOW TABLES显然是错误的。

但是Snowflake的文档中，对SHOW TABLES还有一些参数可选：

>[ IN ... ]  
&emsp;Optionally specifies the scope of the command. Specify one of the following:  
&emsp;  
&emsp;**`DATABASE`**,  
&emsp;**`DATABASE <db_name>`**  
&emsp;&emsp;Returns records for the current database in use or for a specified database (\<db_name\>).  
&emsp;&emsp;If you specify `DATABASE` without \<db_name\> and no database is in use, the keyword has no effect on the output.  
&emsp;  
&emsp;**`Schema`**,  
&emsp;**`SCHEMA <schema_name>`**,  
&emsp;**`<schema_name>`**  
&emsp;&emsp;Returns records for the current schema in use or a specified schema (\<schema_name\>).  
&emsp;&emsp;SCHEMA is optional if a database is in use or if you specify the fully qualified \<schema_name\> (for example, `db.schema`).  
&emsp;&emsp;If no database is in use, specifying `SCHEMA` has no effect on the output.

> References: [https://docs.snowflake.com/en/sql-reference/sql/show-tables#parameters](https://docs.snowflake.com/en/sql-reference/sql/show-tables#parameters)

因此当我们使用如下SQL时：

```sql
SHOW TABLES IN DATABASE;
```

由于未指定数据库，因此使用当前的默认数据库，恰巧和我们期望的范围一致。

返回结果如下：

|**created_on**|**name**|**database_name**|**schema_name**|**kind**|**owner**|
|:--|--|--|--|--|--|
|2024-02-01 23:30:24.534 -0800|TestTable|Snowflake Schema Test|JAVEN|TABLE|ACCOUNTADMIN|
|2024-02-01 23:30:30.178 -0800|TestTable1|Snowflake Schema Test|JAVEN|TABLE|ACCOUNTADMIN|
|2024-02-01 23:29:33.955 -0800|TestTable|Snowflake Schema Test|PUBLIC|TABLE|ACCOUNTADMIN|
|2024-02-01 23:29:42.900 -0800|TestTable1|Snowflake Schema Test|PUBLIC|TABLE|ACCOUNTADMIN|
|2024-02-01 23:30:36.126 -0800|TestTable2|Snowflake Schema Test|PUBLIC|TABLE|ACCOUNTADMIN|

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/SHOW%20TABLES%20in%20Snowflake/SHOW-TABLES-in-Snowflake-3.png)