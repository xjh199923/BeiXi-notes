#### Sql create table 语句
Sql create table 语句用于创建数据库中的表。
表由行和列组成，每个表都必须有个表名。
#### create table 语法

```sql
create table table_name
(
column_name1 data_type(size),
column_name2 data_type(size),
column_name3 data_type(size),
....
);
```
>column_name 参数规定表中列的名称。
data_type 参数规定列的数据类型（例如 varchar、integer、decimal、date 等等）。
size 参数规定表中列的最大长度。

 #### create table 实例
现在我们想要创建一个名为 "Persons" 的表，包含五列：PersonID、Name、Address 和 City。
我们使用下面的  create table语句：
实例

```sql
create table Persons
(
PersonID int,
Name varchar(255),
Address varchar(255),
City varchar(255)
);
```

>PersonID 列的数据类型是 int，包含整数。
Name、Address 和 City 列的数据类型是 varchar，包含字符，且这些字段的最大长度为 255 个字符。

空的 "Persons" 表如下所示：
|  PersonID| Name | Address|  City| 
|--|--|--|--|

在Sql server创建表如图所示
![ ](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pLmxvbGkubmV0LzIwMjAvMDQvMDkvYnlGaDQzWDlvekNmNnZ0LnBuZw?x-oss-process=image/format,png#pic_center)
可使用 insert into 语句向空表写入数据,这个语法我们在后面的教程会讲到。