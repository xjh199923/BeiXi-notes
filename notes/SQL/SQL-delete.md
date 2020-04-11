### Sql delete 语句
delete 语句用于删除表中的记录。delete 语句用于删除表中的行。
#### Sql delete 语法

```sql
delete from table_name
where some_column=some_value;
```
> 请注意 Sql delete 语句中的 where 子句！
where 子句规定哪条记录或者哪些记录需要删除。如果您省略了 where 子句，所有的记录都将被删除！

演示数据库
在本教程中，我们使用Persons这个表来作为演示
Persons表：

|  PersonId| Name | Address|  City| 
|--|--|--|--|
|1 |小明 |Timoteivn |Sandnes |
|2 |小红|Timoteivn |Sandnes |
|3 |小军|Timoteivn |Stavanger |

#### Sql delete 实例
假设我们要从 "Persons" 表中删除名为 "小明" 这个人 。
我们使用下面的 SQL 语句：
实例

```sql
delete from Persons
where Name='小明';
```

执行以上 SQL，再读取 "Persons" 表，数据如下所示：

|  PersonId| Name | Address|  City| 
|--|--|--|--|
|1 |小红|Timoteivn |Sandnes |
|2 |小军|Timoteivn |Stavanger |

#### 删除所有数据
您可以在不删除表的情况下，删除表中所有的行。这意味着表结构、属性、索引将保持不变：

```sql
delete from table_name;
```
或

```sql
delete * from table_name;
```

>注：在删除记录时要格外小心！因为您不能重来！