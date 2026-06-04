---
title: Northwind Database
description: Northwind Database
date: '2023-07-06'
categories:
    - Database
tags:
    - Database
---

# Northwind Database

## Categories (类别表)

| ColumnName | Description |
| ---- | ---- |
| CategoryID | 类别ID |
| CategoryName | 类别名 |
| Description | 类别说明 |
| Picture | 产品样本 |

## CustomerCustomerDemo (客户类型表1)

| ColumnName | Description |
| ---- | ---- |
| CustomerID | 客户ID |
| CustomerTypeID | 客户类型ID |

## CustomerDemographics (客户类型表2)

| ColumnName | Description |
| ---- | ---- |
| CustomerTypeID | 客户类型ID |
| CustomerDesc | 客户描述 |

## Customers (客户表)

| ColumnName | Description |
| ---- | ---- |
| CustomerID | 客户ID |
| CompanyName | 公司名称 |
| ContactName | 客户姓名 |
| ContactTitle | 客户头衔 |
| Address | 联系地址 |
| City | 所在城市 |
| Region | 所在地区 |
| PostalCode | 邮编 |
| Country | 国家 |
| Phone | 电话 |
| Fax | 传真 |

## Employees (员工表)

| ColumnName | Description |
| ---- | ---- |
| EmployeeID | 员工ID |
| LastName + FirstName | 员工姓名 |
| Title | 头衔 |
| TitleOfCourtesy | 职称 |
| BirthDate | 出生日期 |
| HireDate | 雇用日期 |
| Address | 家庭地址 |
| City | 所在城市 |
| Region | 所在地区 |
| PostalCode | 邮编 |
| Country | 国家 |
| HomePhone | 家庭电话 |
| Extension | 分机 |
| Photo | 照片 |
| notes | 笔记 |
| ReportsTo | 上级 |
| PhotoPath | 照片路径 |

## EmployeeTerritories (员工部门表)

| ColumnName | Description |
| ---- | ---- |
| EmployeeID | 员工编号 |
| TerritoryID | 部门代号 |

## Order Details (订单明细表)

| ColumnName | Description |
| ---- | ---- |
| OrderID | 订单编号 |
| ProductID | 产品编号 |
| UnitPrice | 单价 |
| Quantity | 订购数量 |
| Discount | 折扣 |

## Orders (订单表)

| ColumnName | Description |
| ---- | ---- |
| OrderID | 订单编号 |
| CustomerID | 客户编号 |
| EmployeeID | 员工编号 |
| OrderDate | 订购日期 |
| RequiredDate | 预计到达日期 |
| ShippedDate | 发货日期 |
| ShipVia | 运货商 |
| Freight | 运费 |
| ShipName | 货主姓名 |
| ShipAddress | 货主地址 |
| ShipCity | 货主所在城市 |
| ShipRegion | 货主所在地区 |
| ShipPostalCode | 货主邮编 |
| ShipCountry | 货主所在国家 |

## Products (产品表)

| ColumnName | Description |
| ---- | ---- |
| ProductID | 产品ID |
| ProductName | 产品名称 |
| SupplierID | 供应商ID |
| CategoryID | 类型ID |
| QuantityPerUnit | 数量 |
| UnitPrice | 单价 |
| UnitsInStock | 库存数量 |
| UnitsOnOrder | 订购量 |
| ReorderLevel | 再次订购量 |
| Discontinued | 中止 |

## Region (地区表)

| ColumnName | Description |
| ---- | ---- |
| RegionID | 地区ID |
| RegionDescription | 地区描述 |

## Shippers (运货商表)

| ColumnName | Description |
| ---- | ---- |
| ShipperID | 运货商ID |
| CompanyName | 公司名称 |
| Phone | 联系电话 |

## Suppliers (供应商表)

| ColumnName | Description |
| ---- | ---- |
| ShipperID | 供应商ID |
| CompanyName | 供应商姓名 |
| Phone | 联系电话 |

## Territories (地域表)

| ColumnName | Description |
| ---- | ---- |
| TerritoryID | 地域编号 |
| TerritoryDescription | 地域描述 |
| RegionID | 地区编号 |