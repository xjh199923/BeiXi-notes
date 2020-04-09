## SQL 约束（Constraints）
SQL 约束用于规定表中的数据规则。如果存在违反约束的数据行为，行为会被约束终止。约束可以在创建表时规定（通过 create table 语句），或者在表创建之后规定（通过 alter table 语句）。

### create table + constraint 语法
```sql
create table table_name
(
column_name1 data_type(size) constraint_name,
column_name2 data_type(size) constraint_name,
column_name3 data_type(size) constraint_name,
....
);
```
> 在 SQL 中，我们有如下约束：
>- not null - 指示某列不能存储 NULL 值。
>- unique - 保证某列的每行必须有唯一的值。
>- primary key - not null 和 unique 的结合。确保某列（或两个列多个列的结合）有唯>一标识，有助于更容易更快速地找到表中的一个特定的记录。
>- foreign key - 保证一个表中的数据匹配另一个表中的值的参照完整性。
>- check - 保证列中的值符合指定的条件。
>- default - 规定没有给列赋值时的默认值

接下来，我们依次给大家分享每一种约束。

### Sql not nul 约束
在默认的情况下，表的列接受 NULL 值。not null 约束强制列不接受 NULL 值。not null 约束强制字段始终包含值。这意味着，如果不向字段添加值，就无法插入新记录或者更新记录。

下面的 SQL 强制 "PersonID" 列、 "Name" 列以及 "Address" 列不接受 NULL 值：
```sql
create table Persons
(
	PersonID int not null,
	Name varchar(255) not null,
	Address varchar(255) not null,
	City varchar(255)
);
```
##### 添加 not null 约束
在一个已创建的表的 "City" 字段中添加 not null 约束如下所示：
实例

```sql
alter table Persons
alter column City varchar(255) not null;
```

#### 删除 not null 约束
在一个已创建的表的 "Age" 字段中删除 NOT NULL 约束如下所示：
实例

```sql
alter table Persons
alter column City varchar(255)  null;
```
> 注意：在添加和删除not null约束，我用change和modify命令始终报错，这是因为我用的是sql server数据库，而change和modify命令是在my sql 和oracle下才能用的语法。

![ ](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9pLmxvbGkubmV0LzIwMjAvMDQvMDkvMjRZbmU5N2ZBTlZCMXlXLnBuZw?x-oss-process=image/format,png#pic_center)

### Sql unique 约束
unique 约束唯一标识数据库表中的每条记录。unique 和primary key约束均为列或列集合提供了唯一性的保证。primary key 约束拥有自动定义的 unique 约束。请注意，每个表可以有多个 unique约束，但是每个表只能有一个 primary key 约束。
#### create table 时的 unique 约束
下面的 SQL 在 "Persons" 表创建时在 "PersonId" 列上创建unique 约束：
###### MySQL：

```sql
create table Persons
(
	PersonId int not null,
	Name varchar(255) not null,
	Address varchar(255),
	City varchar(255),
	unique (PersonID)
);
```

###### SQL Server / Oracle / MS Access：

```sql
create table Persons
(
	PersonId int not null unique,
	Name varchar(255) not null,
	Address varchar(255),
	City varchar(255),
	unique (PersonID)
);
```
如需命名 unique 约束，并定义多个列的 unique 约束，请使用下面的 SQL 语法：
###### MySQL / SQL Server / Oracle / MS Access：

```sql
create table Persons
(
	PersonId int not null,
	Name varchar(255) not null,
	Address varchar(255),
	City varchar(255),
	unique (PersonID),
	constraint uc_PersonID unique (PersonId,Name)
);
```

#### alter 时的 unique 约束
当表已被创建时，如需在 "PersonID" 列创建unique 约束，请使用下面的 SQL：
###### MySQL / SQL Server / Oracle / MS Access：

```sql
alter table Persons
add unique (PersonID)
```
如需命名 UNIQUE 约束，并定义多个列的 UNIQUE 约束，请使用下面的 SQL 语法：
###### MySQL / SQL Server / Oracle / MS Access：

```sql
alter table Persons
add constraint uc_PersonID unique (PersonId,Name)
```

#### 撤销 UNIQUE 约束
如需撤销 UNIQUE 约束，请使用下面的 SQL：
###### MySQL：

```sql
alter table Persons
drop index uc_PersonID
```

###### SQL Server / Oracle / MS Access：

```sql
alter table Persons
drop constraint uc_PersonID
```

### primary key 约束

primary key 约束唯一标识数据库表中的每条记录。主键必须包含唯一的值。主键列不能包含 NULL 值。每个表都应该有一个主键，并且每个表只能有一个主键。
#### create table 时的 primary key 约束
下面的 SQL 在 "Persons" 表创建时在 "PersonID" 列上创建 primary key 约束：
###### MySQL：

```sql
create table Persons
(
	PersonId int not null,
	Name varchar(255) not null,
	Address varchar(255),
	City varchar(255),
	primary key (PersonID)
);
```
###### SQL Server / Oracle / MS Access：
```sql
create table Persons
(
	PersonId int not null primary key,
	Name varchar(255) not null,
	Address varchar(255),
	City varchar(255),
);
```

如需命名 primary key 约束，并定义多个列的 primary key 约束，请使用下面的 SQL 语法：
###### MySQL / SQL Server / Oracle / MS Access：

```sql
create table Persons
(
	PersonId int not null,
	Name varchar(255) not null,
	Address varchar(255),
	City varchar(255),
	constraint pk_PersonID primary key (PersonID,Name)
);
```

注释：在上面的实例中，只有一个主键 primary key（pk_PersonID）。然而，pk_PersonID 的值是由两个列（PersonID和 Name）组成的。
#### alter table 时的 primary key 约束
当表已被创建时，如需在 "PersonId" 列创建 primary key 约束，请使用下面的 SQL：
###### MySQL / SQL Server / Oracle / MS Access：
```sql
alter table Persons
add primary key (PersonID)
```

如需命名 primary key 约束，并定义多个列的 primary key 约束，请使用下面的 SQL 语法：
###### MySQL / SQL Server / Oracle / MS Access：
```sql
alter table Persons
add constraint pk_PersonID primary key (PersonID,Name)
```
注释：如果您使用 alter table 语句添加主键，必须把主键列声明为不包含 NULL 值（在表首次创建时）。
#### 撤销 primary key 约束
如需撤销 primary key 约束，请使用下面的 SQL：
###### MySQL：
```sql
alter table Persons
drop primary key
```
###### SQL Server / Oracle / MS Access：
```sql
alter table Persons
drop constraint pk_PersonID
```

### foreign key 约束
一个表中的 foreign key 指向另一个表中的 unique key(唯一约束的键)。
让我们通过一个实例来解释外键。请看下面两个表：
Persons 表：
|  PersonId| Name | Address|  City| 
|--|--|--|--|
|1 |小明 |Timoteivn |Sandnes |
|2 |小红|Timoteivn |Sandnes |
|3 |小军|Timoteivn |Stavanger |
Orders表：
|OrderId  | OrderNo | PersonId|
|--|--|--|
|  1| 77895 |  3 |
| 2 |  44678|  3 |
| 3 |22456  |  2|
| 4 | 24562 |  1 |

>请注意:
>- Orders"表中的 "PersonId" 列指向 "Persons" 表中的 "PersonId" 列。
>- "Persons" 表中的 "PersonId" 列是 "Persons" 表中的 primary key。
>- "Orders" 表中的 "PersonId" 列是 "Orders" 表中的 foreign key。
>-  foreign key约束用于预防破坏表之间连接的行为。
>-  foreign key约束也能防止非法数据插入外键列，因为它必须是它指向的那个表中的值之一。
#### create table 时的foreign key 约束
下面的 SQL 在 "Orders" 表创建时在 "PersonId" 列上创建 foreign key 约束：
###### MySQL：
```sql
create table Orders
(
	 OrderId int not null,
	 OrderNo int not null,
	 PesonId int,
	 primary key(OrderId),
	 foreign key (PersonId) references Persons(P_Id)
)
```
###### SQL Server / Oracle / MS Access：
```sql
create table Orders
(
	 OrderId int not null primary key,
	 OrderNo int not null,
	 PesonId int foreign key references Persons(P_Id)
)
```

如需命名foreign key 约束，并定义多个列的foreign key约束，请使用下面的 SQL 语法：
###### MySQL / SQL Server / Oracle / MS Access：
```sql
create table Orders
(
	 OrderId int not null,
	 OrderNo int not null,
	 PesonId int,
	 primary key(OrderId),
	 constraint fk_PerOrders foreign key (PersonId) references Persons(P_Id)
)
```
#### alter table时的foreign key约束
当 "Orders" 表已被创建时，如需在 "P_Id" 列创建 foreign key约束，请使用下面的 SQL：
###### MySQL / SQL Server / Oracle / MS Access：

```sql
alter table Orders
add foreign key (PersonId)
references Persons(PersonId)
```

如需命名 foreign key约束，并定义多个列的 foreign key约束，请使用下面的 SQL 语法：
###### MySQL / SQL Server / Oracle / MS Access：
```sql
alter table Orders
add constraint fk_PerOrders
foreign key (PersonId)
references Persons(PersonId)
```

#### 撤销foreign key约束
如需撤销 foreign key约束，请使用下面的 SQL：
###### MySQL：
```sql
alter table Orders
drop foreign key fk_PerOrders
```

###### SQL Server / Oracle / MS Access：

```sql
alter table Orders
drop constraint fk_PerOrders
```
### check 约束
check 约束用于限制列中的值的范围。如果对单个列定义 check 约束，那么该列只允许特定的值。如果对一个表定义 check 约束，那么此约束会基于行中其他列的值在特定的列中对值进行限制。
#### create table 时的check 约束
下面的 SQL 在 "Persons" 表创建时在 "PersonId" 列上创建 check 约束。check 约束规定 "PersonId" 列必须只包含大于 0 的整数。
###### MySQL：

```sql
create table Persons
(
	PersonId int not null,
	Name varchar(255) not null,
	Address varchar(255),
	City varchar(255),
	check (PersonId>0)
)
```

###### SQL Server / Oracle / MS Access：

```sql
create table Persons
(
	PersonId int not null check (PersonId>0),
	Name varchar(255) not null,
	Address varchar(255),
	City varchar(255)  
)
```

如需命名 check 约束，并定义多个列的 check 约束，请使用下面的 SQL 语法：

###### MySQL / SQL Server / Oracle / MS Access：
```sql
create table Persons
(
	PersonId int not null check (PersonId>0),
	Name varchar(255) not null,
	Address varchar(255),
	City varchar(255),  
	constraint chk_Person check (PersonId>0 and City='Sandnes')
)
```

#### alter table 时的 Sql check 约束
当表已被创建时，如需在 "P_Id" 列创建 check 约束，请使用下面的 SQL：
###### MySQL / SQL Server / Oracle / MS Access:

```sql
alter table  Persons
add check (PersonId>0)
```

如需命名 check 约束，并定义多个列的 check 约束，请使用下面的 SQL 语法：
###### MySQL / SQL Server / Oracle / MS Access：

```sql
alter table  Persons
add constraint chk_Person check (PersonId>0 and City='Sandnes')
```

#### 撤销 check 约束
如需撤销 check 约束，请使用下面的 SQL：
###### SQL Server / Oracle / MS Access：
```sql
alter table Persons
drop constraint chk_Person
```

###### MySQL：
```sql
alter table Persons
drop check chk_Person
```
### Sql default 约束
default 约束用于向列中插入默认值。如果没有规定其他的值，那么会将默认值添加到所有的新记录。
#### create table 时的default 约束
下面的 SQL 在 "Persons" 表创建时在 "City" 列上创建 default 约束：
###### My SQL / SQL Server / Oracle / MS Access：

```sql
create table Persons
(
	PersonId int not null check (PersonId>0),
	Name varchar(255) not null,
	Address varchar(255),
	City varchar(255) default 'Sandnes'
)
```

通过使用类似getdata()这样的函数，default 约束也可以用于插入系统值：

```sql
create table Orders
(
	OrderId int not null,
	OrderNo int not null,
	PersonId int,
	OrderDate date default getdata()
)
```

#### alter table 时的default 约束
当表已被创建时，如需在 "City" 列创建 default 约束，请使用下面的 SQL：
###### MySQL：

```sql
alter table Persons
alter City set default 'SANDNES'
```

###### SQL Server / MS Access：

```sql
alter table Persons
add constraint ab_c default 'SANDNES' for City
```

###### Oracle：

```sql
alter table Persons
modify City default 'SANDNES'
```

#### 撤销 default 约束
如需撤销 default 约束，请使用下面的 SQL：
###### MySQL：

```sql
alter table Persons
alter City drop default
```

###### SQL Server / Oracle / MS Access：

```sql
alter table Persons
alter column City drop default
```

