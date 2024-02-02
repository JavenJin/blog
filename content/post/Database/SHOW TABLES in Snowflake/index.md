---
title: SHOW TABLES in Snowflake
description: Snowflake 中的 SHOW TABLES
date: '2024-02-02'
categories:
    - Database
tags:
    - Database
---

# SHOW TABLES in Snowflake

## Problems encountered

Execute the following SQL in Snowflake to query the tables contained in the database.

```sql
SHOW TABLES;
```

When my database structure is as follows:

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

At this point, the result of executing SHOW TABLES is as follows:

|**created_on**|**name**|**database_name**|**schema_name**|**kind**|**owner**|
|:--|--|--|--|--|--|
|2024-02-01 23:30:24.534 -0800|TestTable|Snowflake Schema Test|JAVEN|TABLE|ACCOUNTADMIN|
|2024-02-01 23:30:30.178 -0800|TestTable1|Snowflake Schema Test|JAVEN|TABLE|ACCOUNTADMIN|
|2024-02-01 23:30:36.126 -0800|TestTable2|Snowflake Schema Test|PUBLIC|TABLE|ACCOUNTADMIN|

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/SHOW%20TABLES%20in%20Snowflake/SHOW-TABLES-in-Snowflake-2.png)

Obviously, there are 5 tables in the database, but the query comes up with only 3 tables.

## Cause of the problem

We guessed that it might be because there are renamed tables under different Schema, and Snowflake did the de-duplication. But this is not true, the official explanation for this is as follows:

> In the output, results are sorted by database name, schema name, and then table name. This means results for a database can contain tables from multiple schemas and might break pagination. In order for pagination to work as expected, **you must execute the SHOW TABLES command for a single schema**. You can use the IN SCHEMA \<schema_name\> parameter to the SHOW TABLES command. Alternatively, you can use the schema in the current context by executing a USE SCHEMA command before executing a SHOW TABLES command.

> References: [https://docs.snowflake.com/en/sql-reference/sql/show-tables#usage-notes](https://docs.snowflake.com/en/sql-reference/sql/show-tables#usage-notes)

It means that only executing this SQL against a Schema is supported.

## Solution

When our business must require a single SQL query for all the tables under that database, it is obviously wrong to use SHOW TABLES directly.

But Snowflake's documentation has some optional parameters for SHOW TABLES:

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

So when we use the following SQL:

```sql
SHOW TABLES IN DATABASE;
```

Since no database is specified, the current default database is used, which happens to be in the range we expect.

The return result is as follows:

|**created_on**|**name**|**database_name**|**schema_name**|**kind**|**owner**|
|:--|--|--|--|--|--|
|2024-02-01 23:30:24.534 -0800|TestTable|Snowflake Schema Test|JAVEN|TABLE|ACCOUNTADMIN|
|2024-02-01 23:30:30.178 -0800|TestTable1|Snowflake Schema Test|JAVEN|TABLE|ACCOUNTADMIN|
|2024-02-01 23:29:33.955 -0800|TestTable|Snowflake Schema Test|PUBLIC|TABLE|ACCOUNTADMIN|
|2024-02-01 23:29:42.900 -0800|TestTable1|Snowflake Schema Test|PUBLIC|TABLE|ACCOUNTADMIN|
|2024-02-01 23:30:36.126 -0800|TestTable2|Snowflake Schema Test|PUBLIC|TABLE|ACCOUNTADMIN|

![](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Database/SHOW%20TABLES%20in%20Snowflake/SHOW-TABLES-in-Snowflake-3.png)