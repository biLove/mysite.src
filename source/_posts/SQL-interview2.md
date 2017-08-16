---
title: SQL 面试题(二)
category: 面试
tags: interview
---


# SQL 面试题（二）

## 找出baseball表中，name属性中包含“To”字符的元组

属性表示列名称，元组表示一条数据。本题可以用 like 操作符，以及 SQL 的通配符。

like 操作符用于在 WHERE 子句中搜索列中的指定模式。
like 一般搭配通配符使用
not like 可以选取与指定模式不同的其他值

```sql
SELECT * FROM baseball WHERE name LIKE 'TO%';
// % 是 SQL 的通配符，用来指代1个或多个字符
```

常见的通配符有

通配符 | 含义
--------- | -------------
% | 表示一个或多个字符
- | 表示一个字符
[charlist] | 字符列中的任何单一字符
[^ charlist] 或者 [!charlist]| 不包含在字符列中的任何单一字符

例如，要找出baseball表中，name属性中以“T”或者“N”或者“J”字符开头的所有元组

```
select * from baseball
where name like '[TNJ]%';

// 如果不支持字符列的表达法，可以使用or 或者 and关键词
SELECT * FROM baseball
WHERE name LIKE 'N%' or name like 'T%' or name like 'J%';

//  [!charlist] 可以用not like来满足
```

## 增加一个列

使用 alter 操作符

```sql
alter table test add column Email text;

alter table table_name add column column_name datatype;
```

## 更新表中的数据

为 test 表中，Id=1的元组添加 Email值，值为“10177157@qq.com”
使用 update 操作符

```sql
UPDATE test SET Emali = '10177157@qq.com' WHERE Id =2;
```

## 什么是视图

view 是从真实的基础表 table 里面，根据用户的需要，做成的虚表。

view有以下几个特点：

1. view 中的数据可以来自于多个表；
2. view 的数据会随着真实表格的数据变化而变化；
3. view 生成以后，只能使用select查询，不能用update、delete、insert来修改虚拟表的内容
4. view 不同的view可以针对不同需求的人，展示不同的数据，而不必向他们展示所有的数据，可以保持数据的保密性；
5. view 不能进行修改；
6. view 还可以用来简化查询。如果我们经常使用某些数据，就可以把他们做成一个view，每次直接使用 ```select * from view_name``` 就可以了，比每次重新写SQL语句要简单的多；

语法

```sql
CREATE VIEW view_name AS
SELECT column_name(s) FROM table_name
WHERE condition; 
// 建立一个视图 view，从真实表 table_name 中选出满足 condition 条件的数据

DROP VIEW view_name;
// 删除视图 view_name
```

## 什么是索引

索引是一种特殊的查询表，可以用来更快更搞笑的查询数据。索引类似于图书馆的图书目录，可以方便用户更快的找到想要的数据。

不过，由于索引表会跟着数据的更新而更新，所以，如果数据表经常更新数据或插入、删除数据，则不适合建立索引，不然会导致更新表的数据变慢很多。

另外，索引不适合以下情况：

1. 小的数据表不适合使用索引；
2. 频繁更改数据的数据表；
3. 取值单一的数据表中的列不适合作为索引；
4. 列中包含大数或者Null值，不适合作为索引。

语法

```sql
CREATE INDEX index_name
ON table_name;
// 为table_name 建立索引

CREATE INDEX index_name
ON table_name(column_name);
// 为 table_name表中的 column_name列建立索引

CREATE INDEX index_name
ON table_name(column_name1,column_name2,……);
// 聚簇索引，即为多个列建立索引

CREATE UNIQUE INDEX index_name
on table_name (column_name);
// 唯一索引

DROP INDEX index_name;
// 删除索引
```

## SQL中的函数

SQL 拥有很多可用于计数和计算的内建函数。

### 函数的语法

内建 SQL 函数的语法是：

```sql
SELECT function(列) FROM 表
```

### 函数基本类型

主要分为两类，

1. 合计函数（Aggregate function），面对一系列的值，返回一个单一的值
2. Scalar函数：面对一个输入值，返回基于输入值的单一值

#### 合计函数 Aggregate function

合计函数常与group by操作符一起使用，用来分组计数
也可以和 order by 一起使用，来对数据进行排序

1. count(column) 求行数
2. avg 求平均
3. sum 求和
4. min 求最小值
5. max 求最大值
6. count(distinct column) 求不同值的个数

例如：选择视图base中的height列，并将数据按照height分组，计算每组的数量num，并将num按照倒序排列

```sql
SELECT height,count(*) as num
FROM base
GROUP BY height
ORDER BY num DESC;
```

#### Scalar 函数

1. round(column_name, decimals) 将数据舍入为指定小数；
2. Now()，返回当前时间
3. len(column_name)，返回当前字符的长度
4. 其他

## Union 操作符

union 操作符可以**合并**两个或多个select语句，并取不同的值（即会默认去重）。

union all 默认不去重，返回所有的值。

使用union 或 union all时，select语句必须有相同数量的列和数据类型。

union以后，会选择第一个select语句里面的列，作为列名。并将其他select语句里面的值对应插入结果中

例如，我们要将 baseball 表的 name、height 列和 test 表中的 Name、Age 列合并

```sql
select name,height from baseball
union
select Name,Age from test;
```

结果会用 name 和 height 作为列名。

## join

引用两个表时，我们可以使用join和on关键词，也可以直接用where来进行匹配

```sql
SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons, Orders
WHERE Persons.Id_P = Orders.Id_P 

与

SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons
INNER JOIN Orders
ON Persons.Id_P = Orders.Id_P
ORDER BY Persons.LastName

是相同的作用
```

inner join和join的作用是一样的，在表中至少存在一个匹配时，返回行。如果 "Persons" 中的行在 "Orders" 中没有匹配，就不会列出这些行。

### left join

在某些数据库中，left join 也叫做 left out join.

LEFT JOIN 关键字会从左表 (table_name1) 那里返回所有的行，即使在右表 (table_name2) 中没有匹配的行。

**tab1**

id | size
--------- | -------------
1 | 10
2 | 20
3 | 30

**tab2**

size | name
--------- | -------------
10 | aaa
20 | bbb
20 | ccc

我们使用left join来连接 tab1和tab2时，（tab1作为左表），会默认输出tab1的所有行，如果对应tab2中没有匹配的值，则没有值的部分用空值或者null表示。如果对应到tab2中有多个匹配值，则把每个值都打印出来。

```sql
SELECT tab1.id, tab1.size, tab2.name
FROM tab1
LEFT JOIN tab2
ON tab1.size = tab2.size;
```

打印结果如下：

id | size | name
---- | ---- | ----
1 | 10 | aaa
2 | 20 | bbb
2 | 20 | ccc
3 | 30 | <null>

如果反过来，把tab2作为左表，则输出结果为

id | size | name
---- | ---- | ----
1 | 10 | aaa
2 | 20 | bbb
2 | 20 | ccc


### right join

RIGHT JOIN 关键字会右表 (table_name2) 那里返回所有的行，即使在左表 (table_name1) 中没有匹配的行。

与left join的原理类似，不过在sqlite3中，不支持right join和full join，其他数据库可能支持。

### FULL JOIN 

只要其中某个表存在匹配，FULL JOIN 关键字就会返回行。

语法

```sql
SELECT column_name(s)
FROM table_name1
FULL JOIN table_name2 
ON table_name1.column_name=table_name2.column_name
```
注释：在某些数据库中， FULL JOIN 称为 FULL OUTER JOIN。


从上面的分析我们可以知道，join的作用主要是匹配，通过不同表的列之间的关系进行匹配，而union的作用主要是合并，只需要合并的select语句有相同的列数和相似的数据类型就可以进行合并。

也就是，如果我们需要，查询的时候，可以把name和Email合并到同一个列中。

## where 和 on 、having的差别

首先，where 和 on 和 having 都是可以加条件的子句。

### where 和 on 差别

如下表

num |where | on 
---- | ----- | -------------
1 | 在一个表设置过滤条件，或多个表设置过滤条件的情况下都可以用。 | 在两个或多个表连接的时候才能用
2 | where是先进行统计以后，在进行过滤 | on是先把不符合条件的记录过滤后才进行统计
3 | where 和 on比较，where后执行 | where 和 on比较，on 先执行

### where 和 having 的差别

在 SQL 中增加 HAVING 子句原因是，WHERE 关键字无法与合计函数一起使用。

1. 如果要对 合计函数进行过滤，那就要使用 having。
2. 一般来说，having要和合计函数（例如：count、sum、avg、min、max）一起使用，group by 一起使用。
3. 一般是on 最先生效，再是 where进行条件过滤，最后才是计算合计函数，再用having对合计函数筛选。

#### 举例

用 left join 来检验 on 和 where 的差别。
left join 会返回左表所有的行，不论右表能不能匹配条件，如果右表有多个匹配值。

用on的话，是先把不符合条件的记录过滤后才进行统计；
用where的话，系统首先根据各个表之间的联接条件，把多个表合成一个临时表后，再由where进行过滤；

故，对于上述的 tab1 和 tab2，
**如果使用on进行过滤：**

```sql
select *
from tab1
left join tab2
on tab1.size = tab2.size
and tab2.name = 'aaa';
```
这里会先按照 tab1.size = tab2.size 和 条件 tab2.name = 'aaa'进行过滤，再将左右表进行连接，故打印结果如下：

id | size | size | name
---- | ---- | ---- | ---
1 | 10 |10 | aaa 
2 | 20 | <null> | <null>
3 | 30 | <null> | <null>

**如果使用where进行过滤**

```sql
select *
from tab1
left join tab2
on tab1.size = tab2.size
where tab2.name = 'aaa';
```
这里会先按照 tab1.size = tab2.size 将左右表进行连接，再使用where进行条件过滤，故打印结果如下：

id | size | size | name
---- | ---- | ---- | ---
1 | 10 |10 | aaa 


#### 总结

on、where、having 都可以进行过滤，作用的顺序不一样。
on是先过滤再连接；where是先连接，在过滤
having可以和where一起使用，先用where进行条件过滤，再用having进行合计函数过滤。


