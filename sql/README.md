# SQL 学习

假期疫情期间和小邓居家隔离学习 SQL 的时光和成果，宝山在旁边睡觉，嘿嘿。

![宝山在睡觉](./baoshan-sleeping.jpg)

## 1. SQL 基础入门



## 1. SQL Server Management Studio 小技巧

一些使用小技巧，在 SS Management Studio 中的快速使用

### 1.1 SQL 查询编辑器显示行号

Tool > Options > Text Editior > Transact-SQL

### 1.2 SQL 查询大小写快速转换

Editor > Addvanced > Make Uppercase

## 2. SQL 数据库备份与迁移

### 2.1 数据库迁移
     
迁出：数据库-detach分离 注：不会影响源文件
     
迁入：A.找到要备份数据库的mdf文件 B.数据库-右击attach（附加）-添加-导入成工 注：log文件可以删掉，不影响使用   
    
### 2.2 数据库备份

备份：数据库-备份

还原：数据库-还原-添加（bak文件）-导入成功

### 3. 数据类型

整数类型

| 类型 | 描述 |
| ----- | :----- |
| int | 存储范围是-2,147,483,648到2,147,483,647之间的整数，主键列常设置此类型。（每个数值占用 4字节） |
| smallint | 存储范围是-32,768 到 32,767 之间的整数，用来存储限定在特定数值范围内的数据。（每个数值占用 2 字节） |
| tinyint | 存储范围是0到255 之间的整数，用来存储有限数目的数值。（每个数值占用 1 字节）|
| bigint | 存储范围是-9,223,372,036,854,775,808到 9,223,372,036,854,775,807之间的整数。（每个数值占用 8 字节） | 
| bit | 值只能是0或1，当输入0以外的其他值时，系统均把它们当1看待。常用来表示真假、男女等二值选择。 |

数值类型

| 类型 | 描述 |
| ----- | :----- |
| decimal(p,s) | p 为精度（有效位），表示可储存数值的最大位数，小数点左右两侧都包括在内，默认最大位为38 位；s为小数位数，标识小数点后  面所能储存的最大位数，默认最小位为0位。如：123.45,则 p=5，s=2（内存大小取决于精度p） |
| numeric(p,s) | numeric 和 decimal 是功能相同的，同是用来保存精度可变的浮点型数据。 |
| float | 浮点型，它是一种近似数值类型，float(n)可储存1-53的可变精度浮点数值。（内存大小取决于精度n） |
| money | 货币型，能存储从-9220 亿到 9220 亿之间的数据，精确到小数点后四位。（每个数值占用 8 字节） | 

日期时间

| 类型 | 描述 |
| ----- | :----- |
| datetime | 储存有效日期范围是1753/1/1~9999/12/31，可精准到3.33毫秒。（每个数值占用 8 字节） |
| smalldatetime | 储存有效日期范围是1900/1/1~2079/6/6，精确到分钟。（每个数值占用 4 字节） |

字符串类型

| 类型 | 描述 |
| ----- | :----- |
| char(m) | 固定长度字符串，长度为 m。 |
| nchar(m) | 国际化固定长度字符串，长度为 m。 |
| varchar(m) | 可变长度字符串，最大长度为m，且必须是一个介于 1 和 8,000 之间的数值。|
| nvarchar(m) | 国际化可变长度字符串，最大长度为m， 且必须是一个介于 1 和 4,000 之间的数值。 | 
| text | 可变长度字符串，最大长度为 231 - 1个字节。 |
| ntext | 国际化可变长度字符串，最大长度为 230 - 1个字符。 |

## 4.SQL 基础

创建表的方式：SQL Server Management Studio/Transact-SQL
``` SQL
CREATE TABLE USERINFO
(ID int primary key NOT NULL,
name varchar(10) NOT NULL,
age int NULL
)
```
删除表：
```SQL
DROP TABLE tablename
```
更改字段类型长度：
``` SQL
ALTER TABLE USERINFO
ALTER COLUMN name varchar(100)
```
更改字段类型：
``` SQL
ALTER TABLE USERINFO
ALTER COLUMN name float
```
添加not null约束：
```SQL
ALTER TABLE USERINFO
ALTER COLUMN name varchar(100) NOT NULL
```
设置主键：
```SQL
ALTER TABLE USERINFO
ADD CONSTRAINT 主键名 PRIMARY KEY(字段名)
```
更改字段名：
```SQL
EXEC sp_rename '表名.字段名','更改后的字段','COLUMN'
```
添加字段名：
```SQL
ALTER TABLE USERINFO
ADD grade varchar(10) not null
```
删除表：
```SQL
DROP TABLE 表名
```
## 5.连接查询

### 5.1 内连接

1.SELECT...FROM A,B 的用法:
```sql
A表的每一条记录和B表的没一条记录连接一遍，形成的临时表：AB表的行数乘积，AB表的列数之和（笛卡尔机）
```
2.SELECT...FROM A,B WHERE...的用法：
```sql
SELECT...FROM A,B 产生的笛卡尔机用 WHERE 中的条件进行过滤
```
3.SELECT...FROM A JOIN B ON...的用法：
```sql
SELECT... FROM A JOIN B 产生的笛卡尔积用 ON 后的条件进行
```


4.SELECT ...FROM A,B WHERE...与SELECT...FROM A JOIN B ON...的比较：
 ```sql
SELECT ...FROM A,B WHERE A.a= B.b 等价于 SELECT...FROM A JOIN B ON A.a=B.b
```
5.SELECT、 FROM、 WHERE、 JOIN、 ON 、GROUP BY、 ORDER、 TOP、 HAVING 的混合使用：

6.习题：

### 6.2 外连接

### 6.3 完全连接
### 6.4 交叉连接
### 6.5 自连接
### 6.6 联合

## 7. 参考资料

[[1] 慕课网：SQL Server基础--T-SQL语句](https://www.imooc.com/learn/435)

[[2] bilibili：SQL Server 2014入门基础课程](https://www.bilibili.com/video/av30388538?p=9)




