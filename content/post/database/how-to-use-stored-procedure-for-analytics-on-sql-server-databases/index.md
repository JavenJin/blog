---
title: How to use Stored Procedure for analytics on SQL Server databases
description: 如何在 SQL Server 数据库中使用Stored Procedure进行分析
date: '2023-11-23'
categories:
    - Database
tags:
    - Database
---

# How to use Stored Procedure for analytics on SQL Server databases

Let's assume that we currently use have a standard Northwind data source ([sql-server-samples/Northwind](https://github.com/microsoft/sql-server-samples/tree/master/samples/ databases/northwind-pubs)).

The Table it contains can be found at: [Northwind Database](https://javenjin.github.io/blog/p/northwind-database/)

It includes the following Table:

- Products

    ```sql
    SELECT
        [ProductID],
        [ProductName],
    |[SupplierID],
    |[CategoryID]
    FROM
        [dbo].[Products];
    ```

    |ProductID|ProductName|SupplierID|CategoryID|
    |:--|--|--|--|
    |1|Chai|1|1|
    |2|Chang|1|1|
    |3|Aniseed Syrup|1|2|
    |4|Chef Anton's Cajun Seasoning|2|2|
    |5|Chef Anton's Gumbo Mix|2|2|
    |6|Grandma's Boysenberry Spread|3|2|
    |7|Uncle Bob's Organic Dried Pears|3|7|
    |8|Northwoods Cranberry Sauce|3|2|
    |9|Mishi Kobe Niku|4|6|
    |10|Ikura|4|8|
    |11|Queso Cabrales|5|4|
    |12|Queso Manchego La Pastora|5|4|
    |13|Konbu|6|8|
    |14|Tofu|6|7|
    |15|Genen Shouyu|6|2|
    |16|Pavlova|7|3|
    |17|Alice Mutton|7|6|
    |18|Carnarvon Tigers|7|8|
    |19|Teatime Chocolate Biscuits|8|3|
    |20|Sir Rodney's Marmalade|8|3|
    |21|Sir Rodney's Scones|8|3|
    |22|Gustaf's Knäckebröd|9|5|
    |23|Tunnbröd|9|5|
    |24|Guaraná Fantástica|10|1|
    |25|NuNuCa Nuß-Nougat-Creme|11|3|
    |26|Gumbär Gummibärchen|11|3|
    |27|Schoggi Schokolade|11|3|
    |28|Rössle Sauerkraut|12|7|
    |29|Thüringer Rostbratwurst|12|6|
    |30|Nord-Ost Matjeshering|13|8|
    |31|Gorgonzola Telino|14|4|
    |32|Mascarpone Fabioli|14|4|
    |33|Geitost|15|4|
    |34|Sasquatch Ale|16|1|
    |35|Steeleye Stout|16|1|
    |36|Inlagd Sill|17|8|
    |37|Gravad lax|17|8|
    |38|Côte de Blaye|18|1|
    |39|Chartreuse verte|18|1|
    |40|Boston Crab Meat|19|8|
    |41|Jack's New England Clam Chowder|19|8|
    |42|Singaporean Hokkien Fried Mee|20|5|
    |43|Ipoh Coffee|20|1|
    |44|Gula Malacca|20|2|
    |45|Rogede sild|21|8|
    |46|Spegesild|21|8|
    |47|Zaanse koeken|22|3|
    |48|Chocolade|22|3|
    |49|Maxilaku|23|3|
    |50|Valkoinen suklaa|23|3|
    |51|Manjimup Dried Apples|24|7|
    |52|Filo Mix|24|5|
    |53|Perth Pasties|24|6|
    |54|Tourtière|25|6|
    |55|Pâté chinois|25|6|
    |56|Gnocchi di nonna Alice|26|5|
    |57|Ravioli Angelo|26|5|
    |58|Escargots de Bourgogne|27|8|
    |59|Raclette Courdavault|28|4|
    |60|Camembert Pierrot|28|4|
    |61|Sirop d'érable|29|2|
    |62|Tarte au sucre|29|3|
    |63|Vegie-spread|7|2|
    |64|Wimmers gute Semmelknödel|12|5|
    |65|Louisiana Fiery Hot Pepper Sauce|2|2|
    |66|Louisiana Hot Spiced Okra|2|2|
    |67|Laughing Lumberjack Lager|16|1|
    |68|Scottish Longbreads|8|3|
    |69|Gudbrandsdalsost|15|4|
    |70|Outback Lager|7|1|
    |71|Flotemysost|15|4|
    |72|Mozzarella di Giovanni|14|4|
    |73|Röd Kaviar|17|8|
    |74|Longlife Tofu|4|7|
    |75|Rhönbräu Klosterbier|12|1|
    |76|Lakkalikööri|23|1|
    |77|Original Frankfurter grüne Soße|12|2|

It contains the following two Stored Procedures:

- TenMostExpensiveProducts

    ```sql
    create procedure "Ten Most Expensive Products" AS
    SET ROWCOUNT 10
    SELECT Products.ProductName AS TenMostExpensiveProducts, Products.UnitPrice
    FROM Products
    ORDER BY Products.UnitPrice DESC;
    ```

    ```sql
    EXEC [dbo].[Ten Most Expensive Products];
    ```

    |TenMostExpensiveProducts|UnitPrice|
    |:--|--|
    |Côte de Blaye|263.5000|
    |Thüringer Rostbratwurst|123.7900|
    |Mishi Kobe Niku|97.0000|
    |Sir Rodney's Marmalade|81.0000|
    |Carnarvon Tigers|62.5000|
    |Raclette Courdavault|55.0000|
    |Manjimup Dried Apples|53.0000|
    |Tarte au sucre|49.3000|
    |Ipoh Coffee|46.0000|
    |Rössle Sauerkraut|45.6000|

- CustOrderHist

    ```sql
    CREATE PROCEDURE CustOrderHist @CustomerID nchar(5)
    AS
    SELECT ProductName, Total=SUM(Quantity)
    FROM Products P, [Order Details] OD, Orders O, Customers C
    WHERE C.CustomerID = @CustomerID
    AND C.CustomerID = O.CustomerID AND O.OrderID = OD.OrderID AND OD.ProductID = P.ProductID
    GROUP BY ProductName
    ```

    ```sql
    EXEC "CustOrderHist" @CustomerID = 'ALFKI';
    ```

    |ProductName|Total|
    |:--|--|
    |Aniseed Syrup|6|
    |Chartreuse verte|21|
    |Escargots de Bourgogne|40|
    |Flotemysost|20|
    |Grandma's Boysenberry Spread|16|
    |Lakkalikööri|15|
    |Original Frankfurter grüne Soße|2|
    |Raclette Courdavault|15|
    |Rössle Sauerkraut|17|
    |Spegesild|2|
    |Vegie-spread|20|

We can't do a join operation on Stored Procedure directly, so there are two options to solve the problem.

## Using DECLARE

```sql
DECLARE @TenMostExpensiveProducts TABLE (
    [TenMostExpensiveProducts] nvarchar(40),
    [UnitPrice] money
);

INSERT INTO
    @TenMostExpensiveProducts EXEC [dbo].[Ten Most Expensive Products];

SELECT
    [Products].[ProductID],
    [Ten Most Expensive Products].[TenMostExpensiveProducts],
    [Ten Most Expensive Products].[UnitPrice],
    [Products].[SupplierID],
    [Products].[CategoryID]
FROM
    @TenMostExpensiveProducts [Ten Most Expensive Products]
    LEFT JOIN
    [dbo].[Products] [Products]
    ON
    [Ten Most Expensive Products].[TenMostExpensiveProducts] = [Products].[ProductName];
```

|ProductID|TenMostExpensiveProducts|UnitPrice|SupplierID|CategoryID|
|:--|--|--|--|--|
|38|Côte de Blaye|263.5000|18|1|
|29|Thüringer Rostbratwurst|123.7900|12|6|
|9|Mishi Kobe Niku|97.0000|4|6|
|20|Sir Rodney's Marmalade|81.0000|8|3|
|18|Carnarvon Tigers|62.5000|7|8|
|59|Raclette Courdavault|55.0000|28|4|
|51|Manjimup Dried Apples|53.0000|24|7|
|62|Tarte au sucre|49.3000|29|3|
|43|Ipoh Coffee|46.0000|20|1|
|28|Rössle Sauerkraut|45.6000|12|7|

```sql
DECLARE @CustOrderHist TABLE (
    [ProductName] nvarchar(40),
    [Total] int
);

INSERT INTO
    @CustOrderHist EXEC [dbo].[CustOrderHist] @CustomerID = 'ALFKI';

SELECT
    [Products].[ProductID],
    [CustOrderHist].[ProductName],
    [CustOrderHist].[Total],
    [Products].[SupplierID],
    [Products].[CategoryID]
FROM
    @CustOrderHist [CustOrderHist]
    LEFT JOIN
    [dbo].[Products] [Products]
    ON
    [CustOrderHist].[ProductName] = [Products].[ProductName];
```

|ProductID|ProductName|Total|SupplierID|CategoryID|
|:--|--|--|--|--|
|3|Aniseed Syrup|6|1|2|
|39|Chartreuse verte|21|18|1|
|58|Escargots de Bourgogne|40|27|8|
|71|Flotemysost|20|15|4|
|6|Grandma's Boysenberry Spread|16|3|2|
|76|Lakkalikööri|15|23|1|
|77|Original Frankfurter grüne Soße|2|12|2|
|59|Raclette Courdavault|15|28|4|
|28|Rössle Sauerkraut|17|12|7|
|46|Spegesild|2|21|8|
|63|Vegie-spread|20|7|2|

## Using Temporal tables

```sql
CREATE TABLE #TenMostExpensiveProducts (
    [TenMostExpensiveProducts] nvarchar(40),
    [UnitPrice] money
);

INSERT INTO
    #TenMostExpensiveProducts EXEC [dbo].[Ten Most Expensive Products];

SELECT
    [Products].[ProductID],
    [Ten Most Expensive Products].[TenMostExpensiveProducts],
    [Ten Most Expensive Products].[UnitPrice],
    [Products].[SupplierID],
    [Products].[CategoryID]
FROM
    #TenMostExpensiveProducts [Ten Most Expensive Products]
    LEFT JOIN
    [dbo].[Products] [Products]
    ON
    [Ten Most Expensive Products].[TenMostExpensiveProducts] = [Products].[ProductName];
```

|ProductID|TenMostExpensiveProducts|UnitPrice|SupplierID|CategoryID|
|:--|--|--|--|--|
|38|Côte de Blaye|263.5000|18|1|
|29|Thüringer Rostbratwurst|123.7900|12|6|
|9|Mishi Kobe Niku|97.0000|4|6|
|20|Sir Rodney's Marmalade|81.0000|8|3|
|18|Carnarvon Tigers|62.5000|7|8|
|59|Raclette Courdavault|55.0000|28|4|
|51|Manjimup Dried Apples|53.0000|24|7|
|62|Tarte au sucre|49.3000|29|3|
|43|Ipoh Coffee|46.0000|20|1|
|28|Rössle Sauerkraut|45.6000|12|7|

```sql
CREATE TABLE #CustOrderHist (
	[ProductName] nvarchar(40),
	[Total] int
);

INSERT INTO 
    #CustOrderHist EXEC [dbo].[CustOrderHist] @CustomerID = 'ALFKI';

SELECT
	[Products].[ProductID],
	[CustOrderHist].[ProductName],
	[CustOrderHist].[Total],
	[Products].[SupplierID],
	[Products].[CategoryID]
FROM
	#CustOrderHist [CustOrderHist]
	LEFT JOIN
	[dbo].[Products] [Products]
	ON
	[CustOrderHist].[ProductName] = [Products].[ProductName];
```

|ProductID|ProductName|Total|SupplierID|CategoryID|
|:--|--|--|--|--|
|3|Aniseed Syrup|6|1|2|
|39|Chartreuse verte|21|18|1|
|58|Escargots de Bourgogne|40|27|8|
|71|Flotemysost|20|15|4|
|6|Grandma's Boysenberry Spread|16|3|2|
|76|Lakkalikööri|15|23|1|
|77|Original Frankfurter grüne Soße|2|12|2|
|59|Raclette Courdavault|15|28|4|
|28|Rössle Sauerkraut|17|12|7|
|46|Spegesild|2|21|8|
|63|Vegie-spread|20|7|2|