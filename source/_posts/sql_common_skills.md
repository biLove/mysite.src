---
title: SQL操作方法
date: 
category: 数据分析
tags: hexo
---

# 数据库

## 数据库规范

规范化是数据库设计的核心思想，规范化涉及在数据库的表格中建立关系，对有关系但是存在于不同表中的数据进行匹配。
数据规范化表格的规则如下：

1. 每行拥有的列数相同，如果有两个值主键相同，我们要将其分成不同的行；
2. 表格的一列或多列组成键，它确定每行要表示什么；
3. 在一个规范化表格中，非键列对键进行描述，它们不描述其他非键列；
4. 在一个规范化表格中，行不会对不存在关系的数据暗示其关系

## SQL

SQL是专为数据库而建立的操作命令集，是一种功能齐全的数据库语言。

### 数据类型
#### 文本和字符串型

text — 任意长度的字符串，如 Python str 或 unicode 类型。

char(n) — 恰好为 n 个字符的字符串。

varchar(n) — 最多 n 个字符的字符串。

#### 数值型

integer — 整数值，如 Python int。

real — 浮点值，如 Python float。精确到 6 位小数。

double precision — 高精度浮点值。 精确到 15 位小数。

decimal — 准确小数值。   

#### 日期和时间型

date — 日历日期，包括年、月、日。

time — 时间。

timestamp — 日期和时间。

# 访问数据库

## SQLite

SQLite 是一个关系数据库管理系统。
操作数据库之前，我们使用SQLite 的 sqlite3 命令被用来创建新的 SQLite 数据库。

```bash
$sqlite3 DatabaseName.db
```

通过此命令，可以进入sqlite管理系统中，链接DatabaseName.db数据库。

### 尝试一些基本的命令行操作

#### 查看数据库

查看sqlite中的数据库

```
.database
```

#### help

无论如何，都可以输入.help命令，以获取可用的命令行操作的清单

#### table

数据.table可以看到数据库中的所有数据表。

#### schema

输入.schema table_name，可以看到表格的架构

#### exit

当操作完成时，输入.exit，退出数据库

## 创建数据库

如果数据库之前没有被创建，在使用如下命令后，

```bash
$sqlite3 DatabaseName.db
```

会直接创建一个名为 ```DatabaseName.db``` 的数据库。

也可用sql创建数据库

```
CREATE DATABASE 数据库名称
```

## 创建数据表

```
CREATE TABLE 表名称
(
列名称1 数据类型,
列名称2 数据类型,
.......
)
```

使用上述方法创建数据表，常见数据类型：Text, CHAR(size), VARCHAR(size), INT(size), FLOAT(size,d)

## 删除数据表

```
DROP TABLE table_name;
```

使用上述命令可以删除数据表

## 从CSV文件导入数据

```
sqlite> .mode csv
sqlite> .import baseball_data.csv baseball_data
```

## 更改数据表名称

```
sqlite> alter table old_name rename to newname;
```

# 数据库操作

根据上面的方法，我建立了一个baseball.db的数据库，并建立了一个baseball数据表。

#### 查看总行数

```
select count(*) from baseball;

打印结果：

count(*)
1157
```

#### 找出使用右手，身高在72~75之间，体重最高的5个人的信息

```
select * from baseball
where handedness == 'R' and height >= 72 and height <= 75
order by weight
limit 5;

打印结果：

"Ramon Manon",R,72,150,0.0,0
"Manny Trillo",R,73,150,0.263,61
"Dave Concepcion",R,74,155,0.267,101
"Frank Taveras",R,72,155,0.255,2
"Rafael Vasquez",R,72,160,0.0,0
```




