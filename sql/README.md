# SQL 学习

假期疫情期间和小邓居家隔离学习 SQL 的时光和成果，宝山在旁边睡觉，嘿嘿。

![宝山在睡觉](./baoshan-sleeping.jpg)

## 1. 主要内容

``` SQL
--Topic 1
SELECT <table fields list> 
FROM <table names list>
WHERE <row constraints specification>
GROUP BY <grouping specification>
HAVING <grouping selection specification>
ORDER BY <order rules specification>

--Topic 2
use [AdventureWorks2012]
go

select Top 100 * from [Production].[Product]

SELECT * 
FROM SALES.SALESORDERDETAIL

--Topic 3
select * from [Production].[Product]

select ProductID, Name, ProductNumber, Color, Size, ListPrice 
from Production.Product

select ProductID, Name, ProductNumber, Color, Size, ListPrice 
from Production.Product
order by listprice desc --desc=descending order ; asc=ascending order

select ProductID, Name, ProductNumber, Color, Size, ListPrice 
from Production.Product
order by listprice desc,Name

select ProductID, Name, ProductNumber, Color, Size, ListPrice 
from Production.Product
order by 2

--Topic 4
select ProductID, Name, ProductNumber, isnull(Color,''), isnull(Size,''), ListPrice 
from Production.Product

--Topic 5
select ProductID, Name, ProductNumber, 
isnull(Color,'') as Color, isnull(Size,'') as Size123, --using an alias 
ListPrice 
from Production.Product

select ProductID, Name as ProductName, --using an alias
'The list price for ' + ProductNumber + ' is $ ' + convert(varchar,ListPrice) +'.' ,--using the concatenation to join character end-to-end.
'The list price for ' + ProductNumber + ' is $ ' + convert(varchar,ListPrice) +'.' as [Description] --using brackets to let SQL server conside the strin as a column name
from Production.Product

--Topic 6
select BusinessEntityID,rate from [HumanResources].[EmployeePayHistory]

select BusinessEntityID
,rate*40*52 as AnnualSalary
,round(rate*40*52,1) as AnnualSalary
,round(rate*40*52,0) as AnnualSalary 
from [HumanResources].[EmployeePayHistory]

select BusinessEntityID
,(rate+5)*40*52 as AnnualSalary
from [HumanResources].[EmployeePayHistory]

--Topic 7
select * from [Sales].[SalesOrderHeader]

select * from [Sales].[SalesOrderHeader]
where SalesPersonID=275

select * from [Sales].[SalesOrderHeader]
where SalesOrderNumber='so43670'

select * from [Sales].[SalesOrderHeader]
where TotalDue>5000

select SalesOrderID,OrderDate,SalesPersonID,TotalDue as TotalSales 
from [Sales].[SalesOrderHeader]
where SalesPersonID=275 and TotalDue>5000 --Comparison conditions: =,>,<,>=,<=,<>

select SalesOrderID,OrderDate,SalesPersonID,TotalDue as TotalSales 
from [Sales].[SalesOrderHeader]
where SalesPersonID=275 and TotalDue>5000 and Orderdate between '2005-08-01' and '1/1/2006'

select SalesOrderID,OrderDate,SalesPersonID,TotalDue as TotalSales 
from [Sales].[SalesOrderHeader]
where SalesPersonID=275 and TotalDue>5000 and Orderdate >= '2005-08-01' and Orderdate < '1/1/2006'

select * from [Production].[Product]
where name ='Mountain-100 Silver, 38'

--Topic 8
select * from [Production].[Product]
where name like'Mountain'

select * from [Production].[Product]
where name like'%Mountain%' --Wildcard % matches any zero or more characters

select * from [Production].[Product]
where name like'mountain%' -- "_" matches any single character

select * from [Production].[Product]
where name like'_ountain%'

--Topic 9
select * from [Production].[Product]
where color in ('red','white','black')

select * from [Production].[Product]
where size in ('60','61','62')

select * from [Production].[Product]
where class not in ('H') -- same as using: <> 'H'

--Topic 10
select * from [Production].[Product]
where size is null

select * from [Production].[Product]
where size is not null

--Topic 11
select * from [Production].[Product]
where color ='white'or color ='black'

select * from [Production].[Product]
where color ='white'and color ='black'

select SalesOrderID,OrderDate,SalesPersonID,TotalDue as TotalSales 
from [Sales].[SalesOrderHeader]
where (SalesPersonID=275 or SalesPersonID=278)  and TotalDue>5000

--Topic 12
select count(SalesPersonID)
from [Sales].[SalesOrderHeader]
where SalesPersonID is not null

select distinct(SalesPersonID)
from [Sales].[SalesOrderHeader]
where SalesPersonID is not null

select count(distinct(SalesPersonID))
from [Sales].[SalesOrderHeader]
where SalesPersonID is not null

--Topic 13
select 
Avg(TotalDue) as AverageTotalSales --aggregate functions
from [Sales].[SalesOrderHeader]

select 
Avg(TotalDue) as AverageTotalSales
,Min(TotalDue) as MinimumTotalSales  
,Max(TotalDue) as MaximumTotalSales
,Sum(TotalDue) as SummaryTotalSales
from [Sales].[SalesOrderHeader]

select SalesPersonID,Max(TotalDue) as MaximumTotalSales 
from [Sales].[SalesOrderHeader] 
--Error Message: Column 'Sales.SalesOrderHeader.SalesPersonID' is invalid in the select list 
--because it is not contained in either an aggregate function or the GROUP BY clause.

select SalesPersonID,Max(TotalDue) as MaximumTotalSales 
from [Sales].[SalesOrderHeader]
where SalesPersonID is not null
group by SalesPersonID
order by SalesPersonID

select SalesPersonID,OrderDate,Max(TotalDue) as MaximumTotalSales 
from [Sales].[SalesOrderHeader]
where SalesPersonID is not null
group by SalesPersonID,OrderDate --Remember to put all un-aggregated columns after "group by"!!!
order by SalesPersonID

select SalesPersonID,OrderDate,Max(TotalDue) as MaximumTotalSales 
from [Sales].[SalesOrderHeader]
where SalesPersonID is not null
group by SalesPersonID,OrderDate 
having Max(TotalDue)>150000
order by SalesPersonID

----The classical T-SQL query!!!
select SalesPersonID,OrderDate,Max(TotalDue) as MaximumTotalSales 
from [Sales].[SalesOrderHeader]
where SalesPersonID is not null and OrderDate >='2007/1/1'
group by SalesPersonID,OrderDate 
having Max(TotalDue)>150000
order by OrderDate desc

```

## 2. SQL Server Management Studio 小技巧

一些使用小技巧，在 SS Management Studio 中的快速使用

### 2.1 SQL 查询编辑器显示行号

Tool > Options > Text Editior > Transact-SQL

### 2.2 SQL 查询大小写快速转换

Editor > Addvanced > Make Uppercase

## 3. 参考资料

[慕课网：SQL Server基础--T-SQL语句](https://www.imooc.com/learn/435)




