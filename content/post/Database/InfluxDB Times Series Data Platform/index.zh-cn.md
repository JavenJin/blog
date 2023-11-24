---
title: InfluxDB 时间序列数据平台
description: InfluxDB Times Series Data Platform
date: '2023-11-24'
categories:
    - Database
tags:
    - Database
---

# InfluxDB 时间序列数据平台

InfluxDB属于时序数据库。

## InfluxDB的数据元素

https://docs.influxdata.com/influxdb/v2.1/reference/key-concepts/data-elements/

|_time|_measurement|location|scientist|_field|_value|
|--|--|--|--|--|--|
|2019-08-18T00:00:00Z|census|klamath|anderson|bees|23|
|2019-08-18T00:00:00Z|census|portland|mullen|ants|30|
|2019-08-18T00:06:00Z|census|klamath|anderson|bees|28|
|2019-08-18T00:06:00Z|census|portland|mullen|ants|32|

- 时间戳(timestamp)

    所有存储在InfluxDB的数据都有一个\_time列，用来存储时间戳。

- 测量(measurement)

    \_measurement列显示测量的名称。测量的名称是字符串。一个测量作为tag、field和timestamp的容器。

- 字段(field)

    一个字段包括存储在\_field列的字段键和存储在\_value列的字段值。一个测量至少需要一个字段。

- 字段键(field key)

    字段键是一个字符串，代表字段的名称。在上面的样本数据中，bees和ants是字段键。

- 字段值(field value)

    一个字段值代表一个相关字段的值。字段值可以是字符串、浮点数、整数或布尔值。样本数据中的字段值显示了指定时间的蜜蜂数量：23和28，以及指定时间的蚂蚁数量：30和32。

- 字段集(field set)

    一个字段集是一个与时间戳相关的字段键值对的集合。一个测量至少需要一个字段。样本数据包括以下字段集：

    ```
    census bees=23i,ants=30i 1566086400000000000
    census bees=28i,ants=32i 1566086760000000000
            -----------------
                Field set
    ```

- 标签(tags)

    标签包括标签键和标签值，以字符串形式存储。

- 标签键(tag key)

    样本数据中的标签键是location和scientist。

- 标签值(tag value)

    标签键location有两个标签值：klamath和portland。标签键scientist也有两个标签值：Anderson和Mullen。

- 标签集(tag set)

    标签的键值对的集合构成了一个标签集。样本数据包括以下四个标签集。

    ```
    location = klamath, scientist = anderson
    location = portland, scientist = anderson
    location = klamath, scientist = mullen
    location = portland, scientist = mullen
    ```
    
- 系列(series)

    一个系列键是共享一个测量、标签集和字段键的点的集合。例如，样本数据包括两个独特的系列键。

    |_measurement|tag set|_field|
    |--|--|--|
    |census|location=klamath,scientist=anderson|bees|
    |census|location=portland,scientist=mullen|ants|
    
    一个系列包括时间戳和给定系列键的字段值。从样本数据来看，这里有一个系列键和相应的系列。

    ```
    # series key
    census,location=klamath,scientist=anderson bees

    # series
    2019-08-18T00:00:00Z 23
    2019-08-18T00:06:00Z 28   
    ```

## C#的InfluxDB库

支持C#的InfluxDB库由官方维护：influxdb-client-csharp(https://github.com/influxdata/influxdb-client-csharp)

- 该官方库不支持SQL语言，而使用了官方提出的Flux语言。

- InfluxDB可以使用InfluxQL和Flux以及api查询数据。

- InfluxQL语言与SQL语言非常相似，但它似乎只用于api查询使用。

- InfluxQL和Flux在功能上基本等同。只有代码看起来不同。（https://docs.influxdata.com/influxdb/v2.1/reference/syntax/flux/flux-vs-influxql/#influxql-and-flux-parity）

## Flux

Flux是一种开源的功能性数据脚本语言（https://docs.influxdata.com/flux/v0.x/）
   
- show databases

    ```
    buckets()
    ```

- show tables

    ```
    import "influxdata/influxdb/schema"

    schema.measurements(bucket: "javen")
    ```

- show columns （需要手动添加\_time和\_value）

    ```
    import "influxdata/influxdb/sample"

    sample.data(set: "sampleTableName")
        |> keys()
        |> keep(columns: ["_value"])
        |> distinct()
    ```

## 数据类型

|InfluxDB datatype|C# datatype|
|--|--|
|dateTime:RFC3339|DateTimeOffset|
|dateTime:RFC3339Nano|DateTimeOffset|
|string|String|
|double|Double|
|boolean|Boolean|
|long|Int64|
|unsignedLong|UInt64|
|base64Binary|Byte[]|
|duration|TimeSpan|

## 连接配置

https://github.com/influxdata/influxdb-client-csharp/tree/master/Client#client-connection-string

可以使用一个连接字符串构建一个客户端，该字符串可以包含编码在URL中的InfluxDBClientOptions参数。

```
connectionString = "http://localhost:8086?token=myToken&org=myOrg"
```

支持以下选项：

|Property|default|description|
|--|--|--|
|org|-|default destination organization for writes and queries|
|bucket|-|default destination bucket for writes|
|token|-|the token to use for the authorization|
|logLevel|NONE|rest client verbosity level|
|timeout|10000 ms|socket timeout|
|allowHttpRedirects|false|Configure automatically following HTTP 3xx redirects|
|verifySsl|true|Ignore Certificate Validation Errors when `false`|

The `timeout` supports `ms`, `s` and `m` as unit. Default is milliseconds.
