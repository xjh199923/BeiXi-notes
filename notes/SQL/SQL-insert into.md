#### Sql insert into语句
insert into 语句用于向表中插入新记录。
#### insert into 语法
insert into 语句可以有两种编写形式。
1. 第一种形式无需指定要插入数据的列名，只需提供被插入的值即可：

```sql
insert into table_name
values(value1,value2,value3,...);
```
2. 第二种形式需要指定列名及被插入的值：

```sql
insert into table_name (column1,column2,column3,...)
values (value1,value2,value3,...);
```

#### insert into 实例
在本教程中，我们将使用上一节建立的Persons空表进行演示,假设我们要向 "Persons" 表中插入一个新行。
我们可以使用下面的 SQL 语句：
##### 实例

```sql
insert into Persons(PersonID,Name,Address,City)
values(2001,'小明','ChongQing','Wushan');
```

执行以上 SQL，再读取 "Persons" 表，数据如下图所示：

![ ](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pLmxvbGkubmV0LzIwMjAvMDQvMDkvZGZvVzc2QWpuRUczdVljLnBuZw?x-oss-process=image/format,png#pic_center)

##### 在指定的列插入数据
我们也可以在指定的列插入数据。
下面的 SQL 语句将插入一个新行，但是只在 "PersonID"、和 "Name" 列插入数据：

```sql
insert into Persons(PersonID,Name)
values(2001,'小花');
```

执行以上 SQL，再读取 "Persons" 表，数据如下所示：
![ ](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pLmxvbGkubmV0LzIwMjAvMDQvMDkvSlpLMnY2em1vZWtGZE0zLnBuZw?x-oss-process=image/format,png#pic_center)
