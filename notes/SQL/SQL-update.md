### Sql update 语句
update 语句用于更新表中已存在的记录。
#### Sql update 语法
```sql
update table_name
set column1=value1,column2=value2,...
where some_column=some_value;
```

>请注意 Sql update 语句中的 where 子句！
where 子句规定哪条记录或者哪些记录需要更新。如果您省略了where子句，所有的记录都将被更新！

演示数据库
在本教程中，我们使用Persons这个表来作为演示
Persons表：

|  PersonId| Name | Address|  City| 
|--|--|--|--|
|1 |小明 |Timoteivn |Sandnes |
|2 |小红|Timoteivn |Sandnes |
|3 |小军|Timoteivn |Stavanger |

#### Sql update 实例
假设我们要把 "小军" 的 City 更新为Sandnes。
我们使用下面的 SQL 语句：

```sql
update City 
set City='Sandnes'
where Name='小军';
```

执行以上 SQL，再读取 "Persons" 表，数据如下所示：

|  PersonId| Name | Address|  City| 
|--|--|--|--|
|1 |小明 |Timoteivn |Sandnes |
|2 |小红|Timoteivn |Sandnes |
|3 |小军|Timoteivn |Sandnes|

>update 警告！
在更新记录时要格外小心！在上面的实例中，如果我们省略了 where 子句，如下所示：

```sql
update City 
set City='Sandnes'
```

执行以上代码会将 Persons表中所有数据的 City改为Sandnes。
执行没有 where 子句的 update 要慎重，再慎重。