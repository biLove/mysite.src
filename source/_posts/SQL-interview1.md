---
title: SQL 面试题(一)
category: 面试
tags: interview
---

# SQL 面试题(一)

### 从baseball数据表中，选出第20到30条数据

本题应该使用 limit 来完成操作

```sql
select * from baseball limit 19,11;

or 

select * from baseball limit 11 offset 19;
```

这两句的作用是一样的，都是读取第20~30条数据。由于数据表是从0开始的，所以第20条数据的行号是19。20~30条一共有11条数据，故选择的数据条数是11.    

### drop、truncate、delete的差别

在SQL中，这三个关键词的作用都是用来删除，但是存在一些差别

1. drop用来删除整个表格，包括表的结构、依赖和数据；truncate和delete用来删除表格中所有的数据，不删除表的结构；
2. truncate用来删除表格中所有数据，delete可以结合where来使用，删除选中的数据，若不结合where使用，则也是删除表格中所有数据；
3. drop和truncate属于DDL（data define language数据库定义语音），操作直接生效，不会放到rollback segment中，故不能回滚；
4. delete属于DML（Data Manipulation Language数据库操作语音），操作会被放到rollback segment中，事务提交后才能生效，也就是需要commit，故可以回滚；
5. 运行速度上，一般drop > truncate > delete;
6. 表和索引所占空间。当表被TRUNCATE 后，这个表和索引所占用的空间会恢复到初始大小，而DELETE操作不会减少表或索引所占用的空间。drop语句将表所占用的空间全释放掉。

操作语句

```sql
delete from table_name where colum_name = 'str';
// 可以删除所有 colum_name = 'str'的行

delete from table_name;
// 可以删除该表中所有数据，保留表的结构和依赖

drop table table_name;
// 删除数据表 table_name，包括表结构，依赖和数据，并释放所占空间

// 在sqlite3中，没有truncate关键词，可以使用delete或者drop代替truncate进行操作；
```

### drop、delete与truncate分别在什么场景之下使用？

不再需要一张表的时候，用drop
想删除部分数据行时候，用delete，并且带上where子句
保留表而删除所有数据的时候用truncate

### 表格名称有空格时，如何修改表格名称？

可以用单引号将表格名称括起来，作为一个整体。例如表格名称为 Titanic Data ，要改名为 titanic

```sql
alter table 'Titanic Data' rename to titanic;
```

用alter来更改表格的名称。alter是DDL语言，立即生效。

### 超键、候选键、主键、外键分别是什么？

首先，定义如下：

超键(super key):在关系中能唯一标识元组的**属性集**称为关系模式的超键，超键包含候选键和主键；  

候选键(candidate key):不含有多余属性的超键称为候选键；候选键是可以作为唯一标识的属性；候选键包含主键；   

主键(primary key):用户选作元组标识的一个候选键称为主键，主键是从候选键中选出来的，是人为定义的。   

外键(foreign key)：如果关系模式其他表的主键，可以作为当前表的外键，主要用来描述两个表的关系。

（其中，元组指数据表中的一行，也就是一条记录。在数据表中，每行是一个元组，每列是一个属性。）

#### 结合实例的具体解释：

假设有如下两个表：
学生（学号，姓名，性别，身份证号，教师编号）
教师（教师编号，姓名，工资）

超键：
由超键的定义可知，学生表中含有学号或者身份证号的任意组合都为此表的超键。如：（学号）、（学号，姓名）、（身份证号，性别）等。

候选键：
候选键属于超键，它是最小的超键，就是说如果再去掉候选键中的任何一个属性它就不再是超键了。学生表中的候选键为：（学号）、（身份证号）。

主键：
主键就是候选键里面的一个，是人为规定的，例如学生表中，我们通常会让“学号”做主键，教师表中让“教师编号”做主键。

外键：
外键比较简单，学生表中的外键就是“教师编号”。外键主要是用来描述两个表的关系。


### 什么是事务？

事务（Transaction）是并发控制的基本单位。所谓的事务，它是一个操作序列，这些操作要么都执行，要么都不执行，它是一个不可分割的工作单位。事务是数据库维护数据一致性的单位，在每个事务结束时，都能保持数据一致性。

DML的操作都需要事务提交后才能生效，也就是需要commit。
DML是数据库操作语言 Data Manipulation Language，包括select、insert、update、delete

事务就是一系列的操作语言组成的操作序列，当我们commit之后，就可以运行。

```sql
// 选出表中所有的数据
SELECT * FROM table_name;
// 我们可以使用 where 来设置筛选条件，用order by对数据进行排序，用limit来设置需要的数据条数和数据开始的索引，用 distinct 来对数据去重


// 插入一条数据
INSERT INTO table_name VALUES (值1，值2，……);
or 
INSERT INTO table_name (列1，列2，……) VALUES (值1，值2，……);
// 使用方法一时，需要给每列都赋值，使用方法二时，可以选择需要插入数据的列，以及对应插入的值，主键必须要有数据

DELETE FROM table_name WHERE colum_name = ‘str’;
// 删除colum_name列中，所有等于str的行

DELETE FROM table_name;
// 删除所有的行

// update用来修改表中的数据
UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值

UPDATE Person SET FirstName = 'Fred' WHERE LastName = 'Wilson' ;
// 如果 Lastname 为 'Wilson' 的元组的 FirstName为空，则新添 FirstName值，如果 FirstName 已经有值了，则更新 FirstName 的值

UPDATE Person SET Address = 'Zhongshan 23', City = 'Nanjing'
WHERE LastName = 'Wilson';
// 此处是设置多列的情况

```


