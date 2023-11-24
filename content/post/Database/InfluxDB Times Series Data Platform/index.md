---
title: InfluxDB Times Series Data Platform
description: InfluxDB 时间序列数据平台
date: '2023-11-24'
categories:
    - Database
tags:
    - Database
---

# InfluxDB Times Series Data Platform

InfluxDB is a temporal database.

## Data Elements for InfluxDB

https://docs.influxdata.com/influxdb/v2.1/reference/key-concepts/data-elements/

|_time|_measurement|location|scientist|_field|_value|
|--|--|--|--|--|--|
|2019-08-18T00:00:00Z|census|klamath|anderson|bees|23|
|2019-08-18T00:00:00Z|census|portland|mullen|ants|30|
|2019-08-18T00:06:00Z|census|klamath|anderson|bees|28|
|2019-08-18T00:06:00Z|census|portland|mullen|ants|32|

- timestamp

    All data stored in InfluxDB has a _time column that stores timestamps.

- measurement

    The _measurement column shows the name of the measurement. Measurement names are strings. A measurement acts as a container for tags, fields, and timestamps.

- field

    A field includes a field key stored in the _field column and a field value stored in the _value column. A measurement requires at least one field.

- field key

    A field key is a string that represents the name of the field. In the sample data above, bees and ants are field keys.

- field value

    A field value represents the value of an associated field. Field values can be strings, floats, integers, or booleans. The field values in the sample data show the number of bees at specified times: 23, and 28 and the number of ants at a specified time: 30 and 32.

- field set

    A field set is a collection of field key-value pairs associated with a timestamp. A measurement requires at least one field. The sample data includes the following field sets:
    
    ```
    census bees=23i,ants=30i 1566086400000000000
    census bees=28i,ants=32i 1566086760000000000
            -----------------
                Field set
    ```

- tags

    Tags include tag keys and tag values that are stored as strings.

- tag key

    The tag keys in the sample data are location and scientist.

- tag value
    
    The tag key location has two tag values: klamath and portland. The tag key scientist also has two tag values: anderson and mullen.

- tag set

    The collection of tag key-value pairs make up a tag set. The sample data includes the following four tag sets:

    ```
    location = klamath, scientist = anderson
    location = portland, scientist = anderson
    location = klamath, scientist = mullen
    location = portland, scientist = mullen
    ```

- series

    A series key is a collection of points that share a measurement, tag set, and field key. For example, the sample data includes two unique series keys.

    |_measurement|tag set|_field|
    |--|--|--|
    |census|location=klamath,scientist=anderson|bees|
    |census|location=portland,scientist=mullen|ants|

    A series includes timestamps and field values for a given series key. From the sample data, here’s a series key and the corresponding series.
    
    ```
    # series key
    census,location=klamath,scientist=anderson bees

    # series
    2019-08-18T00:00:00Z 23
    2019-08-18T00:06:00Z 28   
    ```

## InfluxDB library with C#

The InfluxDB library with C# support is officially maintained: influxdb-client-csharp(https://github.com/influxdata/influxdb-client-csharp)

- The official library does not support the SQL language, but uses the official proposed Flux language.

- InfluxDB can query data using InfluxQL and Flux as well as api.

- The InfluxQL language is very similar to the SQL language, but it seems to be used only for for api query usage.

- InfluxQL and Flux are basically functionally equivalent. Only the code looks different.(https://docs.influxdata.com/influxdb/v2.1/reference/syntax/flux/flux-vs-influxql/#influxql-and-flux-parity)

## Flux

Flux is an open source functional data scripting language(https://docs.influxdata.com/flux/v0.x/)

- show databases

    ```
    buckets()
    ```

- show tables

    ```
    import "influxdata/influxdb/schema"

    schema.measurements(bucket: "bucketsName")
    ```

- show columns (You need to add \_time and \_value manually)

    ```
    import "influxdata/influxdb/sample"

    sample.data(set: "sampleTableName")
        |> keys()
        |> keep(columns: ["_value"])
        |> distinct()
    ```

## Data Type

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

## Connection configuration

https://github.com/influxdata/influxdb-client-csharp/tree/master/Client#client-connection-string

A client can be constructed using a connection string that can contain the InfluxDBClientOptions parameters encoded into the URL.

```
connectionString = "http://localhost:8086?token=myToken&org=myOrg"
```

The following options are supported:

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