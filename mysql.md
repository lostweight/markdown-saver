[TOC]

# 数据库

数据库是计算机用于组织、存储和管理数据的仓库

数据库能够将不同类型的数据，如文本、数字、图像等，以特定的结构排序存储在计算机内，使得使用者能够高效地进行数据查询、修改、删除和分析



## 关系数据库管理系统

数据库可以根据采用地数据结构分成多种类型，常见的数据库是以**表格结构存储数据**，通过SQL管理、控制，这种数据库就是**关系数据库**

**关系数据库是使用行和列组成地二维表格来记录数据**，是目前应用最广泛的一种数据库类型



### SQL

SQL是结构化查询语言的缩写，是一种专门用于操作关系型数据库管理系统的语言

SQL包含一些内置的语法和关键字，我们可以通过编写SQL代码，对数据库中的数据进行查询、插入、更新和删除等操作





### 关系数据库中的表结构



#### 数据表结构

在关系数据库中，**表（table）**是用来组织数据的最基本结构

关系数据库中的表，通常由表***名称、表行***、***表列***  三个部分组成

![img](https://cdn.penpencode.com/upload/06368d128358d5ae10e56f269019bd28/1942x1258/NO.20.png)





##### 表名

一个关系数据库中可以创建多张表，每个表都有一个唯一的名称，用来表示一个特定对象的所有数据

![img](https://cdn.penpencode.com/upload/d45edc2e57ab3c1fe015464937f5e2b3/1424x1062/NO.21.png)





##### 字段（列）

关系数据库将数据按类型分为表中不同的列，这些列称之为***字段*** 。**每个字段均有自己的唯一名字**，用来描述某一对象的特征

例如在用户表中，name字段存储用户的名称、age字段存储用户的年龄、birth字段存储用户的生日

![img](https://cdn.penpencode.com/upload/d8ea6fd83b8170717224f844437e511b/1942x1258/NO.22.png)







##### 数据类型

数据表中**每个字段都会存储一个特定类型的数据**

- 
    国家由文字组成，所以 country字段是字符串（文字、符号组成的数据）类型；
- 字段“数量”由整数组成，所以 count 字段是整数类型；
- 购买日期由日期类型组成，所以 purchase_date 字段是日期类型。



在同一个表中，不同的字段可以有不同的数据类型，但是同一个字段中的数据必须保持一致的数据类型。

![img](https://cdn.penpencode.com/upload/e424028f9958864d8c46555ff06642d7/1694x1198/NO.19.png)

###### 常用的数据类型

关系数据库支持丰富的数据库类型，上图列出了常用的数据类型以及对应的英文名称。



需要特别注意字符与日期、时间数据，它们均需要放在一对单引号`' '`中。其中，日期时间可以使用`'年-月-日 时:分:秒'`的格式表示。

![img](https://cdn.penpencode.com/upload/38cec3c00e4dbbf6f48809de68d749ff/1796x1152/P25.png)







##### 记录（行）



在关系数据库中，通常按行存储数据，每一行包含了表中各列对应的值，这些值组成了一条完整的记录。

![img](https://cdn.penpencode.com/upload/cea67fa07a35005da9b6f4efb680e4d7/1942x1258/NO.222.png)



##### 如何查询一个特定的行**

在用户表中，不同的用户可能使用相同的名称，所以我们无法通过姓名直接定位某一个用户的信息。



此时可以为每个用户记录一个唯一的编号，我们可以通过这个编号快速定位某个用户的信息。﻿

![img](https://cdn.penpencode.com/upload/21a866568cf764e8c915c891d052b8d9/1942x1258/NO.333.png)





###### 主键

为了准确区分每一行，表通常存在一个特殊的列，它每一行都有数据，而且这些数据均不相同，这样特殊的列称为主键（Primary Key），简写为PK。

主键可以唯一标识表中的每一条记录，公安使用身份证号作为公民信息表的主键。

![img](https://cdn.penpencode.com/upload/d7cc69fa1ad7591b3ef7b947e344d03e/1942x1258/NO.3pk.png)





##### **实体关系图（ER图）**

我们通常用形如这样的图形快速描述关系数据库中一个表的结构，这称为实体关系图或ER图。

在ER图中，可以清楚的看到表的名称、字段以及对应的数据类型与主键。

![img](https://cdn.penpencode.com/upload/2059bb4c31b3651ec232ad8d79b56433/688x484/NO.212.png)





### 数据库中的关系

关系数据库中的关系包含两层含义：



#### **1. 表中行与列之间的关系**

在关系表中，行与列存在相互对应的关系。

就是说，只要知道了要查找的字段名称对应的行，就能够定位某个数据。

![img](https://cdn.penpencode.com/upload/cd214377021c9f5c607bbb6618c7c90e/1684x898/NO.36.png)



#### **2. 表与表之间的关系**

在关系数据库中，如果一个表中的某个字段存储着另一个表的主键，那么这两个表就被称为相关表，而这个字段则被称为外键（Foreign Key），简称FK。



举例来说：

在一个数据库中，用户表记录了用户的特征信息，订单表则记录了用户的订单详情。在这种情况下，订单表可能会将用户表的主键存储在一个字段中，通常称为“下单用户”。



这样的设计就建立了用户表和订单表之间的关系。

![img](https://cdn.penpencode.com/upload/7813bcfdda10affbaf2488c1989f4568/2865x1692/NO.31222.png)





#### **设置表关系的意义**

一个用户可能会有多笔订单记录，如果每笔订单都完整地记录了用户的信息，就会导致大量重复和冗余的数据存储。



因此，将数据分解为不同的表，并在它们之间建立关系，不仅可以减少数据的冗余，还能使每个表中的字段更好地反映其特定信息，从而提高数据库的效率和数据的一致性。

![img](https://cdn.penpencode.com/upload/45b33a585669240e1325dd2a293800a6/3222x2505/NO.3ssd8.png)





#### ER图表示表关系

如图所示，在ER图中，我们可以使用带箭头的线条关联有关系的表。

![img](https://cdn.penpencode.com/upload/ed860119ff70035eb417b9496d17cece/2517x1053/NO.39.png)	



![img](https://cdn.penpencode.com/upload/94c53af810d8817d6169241b2bac5758/3200x2476/D1%E6%95%B0%E6%8D%AE%E5%BA%93%E4%B8%8ESQL_%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE.png)







## 创建数据库



![img](https://cdn.penpencode.com/upload/cc63c370d4f651ae8db7fbe72086a412/856x443/%E5%88%9B%E5%BB%BA%E6%95%B0%E6%8D%AE%E5%BA%93.png)

创建一个数据库非常简单，只需要设定数据库的名称与支持存储的字符类型(哪国语言、哪类符号)。先来快速浏览一下代码：



创建一个名为`tshop`的数据库

代码编辑器

```
*-- 创建一个名为tshop的数据库*

CREATE DATABASE tshop CHARSET=utf8mb4;

```



**create**

CREATE 可以帮助我们***声明一次创建***，是一个SQL**关键字**。为了其它非关键字内容区分，这里建议大家使用大写字母书写。



**DATABASE**

是SQL中的另一个关键字，表示数据库

而tshop是新建数据库的名称



**CHARSET=utf8mb4** 可以帮助我们设置数据库使用的编码格式。 它的作用是容许数据库可以正确识别中文、emoji或其它各国的语言与符号。

分号代表该SQL语句在此处结束。不写分号可能造成未知的错误，千万不要忘记它哦~





####   **注释**

注释通常用来解释代码的含义，该行内容会被数据库自动忽略。

在SQL中，使用两个短横线`--`创建一条注释。

![1696831210660](C:\Users\R\AppData\Roaming\Typora\typora-user-images\1696831210660.png)



注：`**SQL 不限制缩进方式**`

与其它编程语言(如Python)不同，SQL语言不限制缩进方式。你可以使用空格、换行等多种方式，调整代码的排版方式，使其更加容易阅读.

SQL可以正常识别下面的代码：

示例1：

```


*-- 使用换行与空格调整代码结构*

CREATE DATABASE 

  tshop 

CHARSET=utf8mb4;


```



示例2：

代码编辑器

```
-- 随意设置换行方式*

CREATE 

DATABASE 

tshop 

CHARSET=utf8mb4;
```



`SQL 关键字不区分大小写`

SQL不区分关键字的大小写，所以`CREATE`与`create`是相同的功能。



虽然如此，在编写SQL代码时，推荐将所有SQL关键字用大写字母表示，可以提高代码的可读性，使其更容易阅读。





## 创建数据表

**确定商品表的字段类型与约束**

使用`CREATE TABLE`可以快速为数据库创建表，在这个过程中需要明确**表的名称**、**字段名**以及该**字段的数据类型**与**约束**：

1. 表名：commodity；
2. 表中四个字段的类型与要求如图所示。





![img](https://cdn.penpencode.com/upload/dc5517f2679f58ae1a410d9359de28a3/1203x624/p17.png)



代码

```
CREATE TABLE tshop.commodity (
	id INT PRIMARY KEY AUTO_INCREMENT, //创建字段id，数据类型为整数。
	name VARCHAR ( 255 ) NOT NULL UNIQUE, //创建name字段，类型为字符串。 设置该字段为非空字段，且该字段中的内容不能重复。
	price DECIMAL(10, 2),   //创建price字段，类型为分数（仅保留小数点后两位，数字最多位数为10位
	create_time DATETIME DEFAULT NOW() //创建create_time字段，类型为日期时间，并使用当前时间为默认值
);



// 其中CREATE为创建某东西的关键词

· TABLE指明要创建的东西为表格

· tshop.commodity指的是在tshop数据库创建一张commodity的数据表

· SQL UNIQUE 约束 UNIQUE 约束唯一标识数据库表中的每条记录

· 关键词decimal(a,b)
         a:指的是整数和小数所能存的最多的位数
         b:指的是小数数字的位数，即a-b就是整数的位数
        
· 提醒，字符与日期有关的数据类型，数据需要放到单引号中哦~

· 设置数据类型的长度（取值范围）
 SQL 还可以指定数据类型的长度。比如：
	VARCHAR(255) 表示该字段最多可以存储255个字符；
	DECIMAL(10, 2) 表示该分数总位数是10，其中最高整数位是8，小数位是2，即存储范围				在-99999999.99~99999999.99的分数。
	
· PRIMARY KEY 主键约束： 用来唯一标识表中的每一条记录，该字段不能有重复或空值。
· AUTO_INCREMENT 自增长约束： AUTO_INCREMENT 会为字段自动生成一个唯一的数字，每添加一行新的数	    据，该数字加1；
· NOT NULL 非空约束： 该约束要求该字段不能出现空值，即必须为该字段添加数据。
· UNIQUE 唯一约束： 用来确保字段中的值不重复，但可以有空值。
· DEFAULT 约束： 用来为字段提供一个默认值，当没有指定值时，就使用默认值。 NOW() 用来获取当前时间，如果没有特意插入时间，就将当前时间存储到字段中。
```

##### **省略数据库名称的小技巧**

当我们需要为数据库创建多个表时，每一条建表语句都需要指定数据库名称，比较麻烦。

为了简化代码，可以借助`USE 数据库名;`提前规定当前要操作的数据库。

```
-- 规定接下的代码均是在操控tshop数据库
USE tshop;
-- 省略tshop，直接写表名
CREATE TABLE commodity (
	id INT PRIMARY KEY AUTO_INCREMENT,
	name VARCHAR ( 255 ) NOT NULL UNIQUE,
	price DECIMAL(10, 2),
	create_time DATETIME DEFAULT NOW()
);
```



##### **编写字段信息**

SQL规定数据库的表中至少包含一个字段，所有的字段信息都记录在一对括号中，这些信息包括：字段的名称、数据类型与约束规则。





### 插入数据

**插入数据的方法**

`INSERT`关键字可以为指定的表插入数据。该关键字提供两种方法：

1. 全列插入：按顺序为表中每一个字段插入数据；
2. 指定列插入：只为特定的列插入数据，其它列填入默认值或空值；

接下来我们以创建好的commodity表为例，分别讲解这两种用法：

![img](https://cdn.penpencode.com/upload/2e6fe873442824405aca415c84f25357/3201x1461/D3%E6%8F%92%E5%85%A5%E6%95%B0%E6%8D%AE.png)





```
INSERT INTO tshop.commodity VALUES 
(1, 'SHARK TEE BLACK', 699, '2023/1/12 12:22:32'),
(2, 'SHARK TEE PINK', 699, '2023/1/12 12:22:32'),
(3, 'SHARK TEE WHITE', 699, '2023/1/12 12:22:32');



· 关键字 INSERT INTO 用于对表格中数据的插入
· 使用INSERT时，需要指定接收数据的表名。 若此时没有选择数据库，还需要使用数据库名.表名的方式
· 关键字VALUES 表示 “值”，也就是需要插入到表格中的数据。
```

**INSERT INTO ... VALUES ...**

当我们想要为某个表格插入数据时，固定格式为**INSERT INTO 表名 VALUES 数据;**

INSERT INTO 支持同时插入多行数据，所以表示“值”的关键字`VALUES`要使用复数形式，别写错了哦~



#### **全列插入数据**

全列插入指的是为表插入数据时，不需要指定要插入的字段名称，只需提供被插入的数据即可。



需要注意：

1. 待插入的所有数据均需要放在一对小括号中，且每个值用逗号隔开；
2. 待插入的数据数量要与字段数量相等，且插入顺序要与建表时的字段顺序一致：

- 对commodity表来说，插入顺序应该为`id、name、price、create_date`。

**日期、时间类型与字符串**

SQL中用来表示日期与字符的数据，都需要放在单引号中。

其中，日期、时间类型通常使用`'年-月-日 时:分:秒'`的格式。





#### **部分列插入**

除了全列插入，我们还可以自由选择要插入数据的字段，即部分列插入。



你可以在`VALUES`前的小括号中，指定数据要插入的字段名称。然后再`VALUES`后给出对应的数据：仅为name与price字段插入数据

```
INSERT INTO tshop.commodity (name, price) VALUES 
('SHARK TEE BLACK', 699),
('SHARK TEE PINK', 699),
('SHARK TEE WHITE', 699);
```





**未被选择的字段**

只对name与price插入数据，其它字段怎么办呢？根据字段的约束规则，会发生以下两种情况：

**1.若约束中有DEFAULT 或 AUTO_INCREMENT ：**

- 因为设置了AUTO_INCREMENT 自增约束，所以id字段会自动将前一行数据的id值+1，作为自己的数据。
- 而create_time设置了DEFAULT 约束，并将默认值设置为 NOW() ，当字段没有接收到数据时，会自动存储当前的日期与时间。



**2.若约束中没有包含DEFAULT 或 AUTO_INCREMENT**

- 若字段没有相关的约束规则，这些字段不会添加如何数据，处于“空”的状态。记为NULL。

![img](https://cdn.penpencode.com/upload/fc86ec46ed66ee80ea992d9d0a0ec94e/1306x654/%E4%BB%A3%E7%A0%81%E6%A8%A1%E6%9D%BF.png)





#### 总结

![img](https://cdn.penpencode.com/upload/fcd53cd8535ad9c9459ad3319dd53be1/2300x1460/Group572.png)

![img](https://cdn.penpencode.com/upload/48f4d85b000bff988884fe091cd4188e/3200x2589/D2%E5%88%9B%E5%BB%BA%E6%95%B0%E6%8D%AE%E5%BA%93%E4%B8%8E%E6%95%B0%E6%8D%AE%E8%A1%A8_%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE.png)

# MySQL

- **SELECT** - 从数据库中提取数据
- **UPDATE** - 更新数据库中的数据
- **DELETE** - 从数据库中删除数据
- **INSERT INTO** - 向数据库中插入新数据
- **CREATE DATABASE** - 创建新数据库
- **ALTER DATABASE** - 修改数据库
- **CREATE TABLE** - 创建新表
- **ALTER TABLE** - 变更（改变）数据库表
- **DROP TABLE** - 删除表
- **CREATE INDEX** - 创建索引（搜索键）
- **DROP INDEX** - 删除索引



## SELECT 语句

SELECT 语句用于从数据库中选取数据。

结果被存储在一个结果表中，称为结果集。

### SQL SELECT 语法

```
SELECT column1, column2, ...
FROM table_name;
```

与

```
SELECT * FROM table_name;
```

**参数说明：**

- **column1, column2, ...**：要选择的字段名称，可以为多个字段。如果不指定字段名称，则会选择所有字段。
- **table_name**：要查询的表名称。

实例：

```
SELECT name,country FROM Websites;
```

![img](https://www.runoob.com/wp-content/uploads/2013/09/98E6B49C-06AF-469B-B907-81C52BBE6BDC.jpg)



## SELECT DISTINCT 语句

在表中，一个列可能会包含多个重复值，有时您也许希望仅仅列出不同（distinct）的值。

DISTINCT 关键词用于返回唯一不同的值。

### SQL SELECT DISTINCT 语法

```
SELECT DISTINCT column1, column2, ...
FROM table_name;
```

**参数说明：**

- **column1, column2, ...**：要选择的字段名称，可以为多个字段。如果不指定字段名称，则会选择所有字段。
- **table_name**：要查询的表名称。

#### SELECT DISTINCT 实例

原表

+----+--------------+---------------------------+-------+---------+
| id | name         | url                       | alexa | country |
+----+--------------+---------------------------+-------+---------+
| 1  | Google       | https://www.google.cm/    | 1     | USA     |
| 2  | 淘宝          | https://www.taobao.com/   | 13    | CN      |
| 3  | 菜鸟教程      | http://www.runoob.com/    | 4689  | CN      |
| 4  | 微博          | http://weibo.com/         | 20    | CN      |
| 5  | Facebook     | https://www.facebook.com/ | 3     | USA     |
+----+--------------+---------------------------+-------+---------+

下面的 SQL 语句仅从 "Websites" 表的 "country" 列中选取唯一不同的值，也就是去掉 "country" 列重复值：

```
SELECT DISTINCT country FROM Websites;
```

![img](https://www.runoob.com/wp-content/uploads/2013/09/E3012A35-35DF-4BBB-8657-8A312C5AEAB6.jpg)





## WHERE 子句

------

WHERE 子句用于过滤记录。

------

### SQL WHERE 子句

WHERE 子句用于提取那些满足指定条件的记录。

### SQL WHERE 语法

```
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

参数说明：

- **column1, column2, ...**：要选择的字段名称，可以为多个字段。如果不指定字段名称，则会选择所有字段。
- **table_name**：要查询的表名称。

```
mysql> SELECT * FROM review_table WHERE word='redo';
+------+-------------+
| word | translation |
+------+-------------+
| redo | v.再做 重做 |
+------+-------------+
1 row in set (0.01 sec)
```





### 文本字段 vs. 数值字段

SQL 使用单引号来环绕文本值（大部分数据库系统也接受双引号）。

在上个实例中 'CN' 文本字段使用了单引号。

如果是数值字段，请不要使用引号。

#### 实例

SELECT * FROM Websites WHERE id=1;

执行输出结果：

![img](https://www.runoob.com/wp-content/uploads/2013/09/639D2956-99CE-44E9-B960-EA14D296820E.jpg)



### WHERE 子句中的运算符

下面的运算符可以在 WHERE 子句中使用：

| 运算符  | 描述                                                       |
| :------ | :--------------------------------------------------------- |
| =       | 等于                                                       |
| <>      | 不等于。**注释：**在 SQL 的一些版本中，该操作符可被写成 != |
| >       | 大于                                                       |
| <       | 小于                                                       |
| >=      | 大于等于                                                   |
| <=      | 小于等于                                                   |
| BETWEEN | 在某个范围内                                               |
| LIKE    | 搜索某种模式                                               |
| IN      | 指定针对某个列的多个可能值                                 |





## AND & OR 运算符

------

AND & OR 运算符用于基于一个以上的条件对记录进行过滤。

------

### SQL AND & OR 运算符

如果第一个条件和第二个条件都成立，则 AND 运算符显示一条记录。

如果第一个条件和第二个条件中只要有一个成立，则 OR 运算符显示一条记录。



### AND 运算符实例

下面的 SQL 语句从 "Websites" 表中选取国家为 "CN" 且alexa排名大于 "50" 的所有网站：

#### 实例

SELECT * FROM Websites WHERE country='CN' AND alexa > 50;

执行输出结果：

![img](https://www.runoob.com/wp-content/uploads/2013/09/and-or1.jpg)

------

### OR 运算符实例

下面的 SQL 语句从 "Websites" 表中选取国家为 "USA" 或者 "CN" 的所有客户：

#### 实例

SELECT * FROM Websites WHERE country='USA' OR country='CN';

执行输出结果：

![img](https://www.runoob.com/wp-content/uploads/2013/09/and-or2.jpg)

------

### 结合 AND & OR

您也可以把 AND 和 OR 结合起来（使用圆括号来组成复杂的表达式）。

下面的 SQL 语句从 "Websites" 表中选取 alexa 排名大于 "15" 且国家为 "CN" 或 "USA" 的所有网站：

实例

SELECT * FROM Websites WHERE alexa > 15 AND (country='CN' OR country='USA');

执行输出结果：

![img](https://www.runoob.com/wp-content/uploads/2013/09/and-or3.jpg)

```
使用的表数据：
+-------------+------------------------+
| word        | translation            |
+-------------+------------------------+
| creatural   | adj.动物的,人的        |
| shaviana    | [复]n.有关萧伯纳的文物 |
| xylographer | n.木刻师,刻版师        |
| redo        | v.再做 重做            |
+-------------+------------------------+
4 rows in set (0.00 sec)

mysql> SELECT * FROM review_table WHERE translation='v.再做 重做' AND word='redo';
+------+-------------+
| word | translation |
+------+-------------+
| redo | v.再做 重做 |
+------+-------------+
1 row in set (0.01 sec)
```





## SQL ORDER BY 关键字

ORDER BY 关键字用于对结果集按照一个列或者多个列进行排序。

ORDER BY 关键字默认按照升序对记录进行排序。如果需要按照降序对记录进行排序，您可以使用 DESC 关键字。

### SQL ORDER BY 语法

```
SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ... ASC|DESC;
```

- **column1, column2, ...**：要排序的字段名称，可以为多个字段。
- **ASC**：表示按升序排序。
- **DESC**：表示按降序排序。

```
+-------------+------------------------+
| word        | translation            |
+-------------+------------------------+
| creatural   | adj.动物的,人的        |
| shaviana    | [复]n.有关萧伯纳的文物 |
| xylographer | n.木刻师,刻版师        |
| redo        | v.再做 重做            |
+-------------+------------------------+
4 rows in set (0.00 sec)

# 普通排序（默认ASC排序）
mysql> SELECT * FROM review_table ORDER BY word;
+-------------+------------------------+
| word        | translation            |
+-------------+------------------------+
| creatural   | adj.动物的,人的        |
| redo        | v.再做 重做            |
| shaviana    | [复]n.有关萧伯纳的文物 |
| xylographer | n.木刻师,刻版师        |
+-------------+------------------------+
4 rows in set (0.01 sec)

# 反向排序
mysql> SELECT * FROM review_table ORDER BY word DESC;
+-------------+------------------------+
| word        | translation            |
+-------------+------------------------+
| xylographer | n.木刻师,刻版师        |
| shaviana    | [复]n.有关萧伯纳的文物 |
| redo        | v.再做 重做            |
| creatural   | adj.动物的,人的        |
+-------------+------------------------+
4 rows in set (0.00 sec)

# 正向排序
mysql> SELECT * FROM review_table ORDER BY word ASC;
+-------------+------------------------+
| word        | translation            |
+-------------+------------------------+
| creatural   | adj.动物的,人的        |
| redo        | v.再做 重做            |
| shaviana    | [复]n.有关萧伯纳的文物 |
| xylographer | n.木刻师,刻版师        |
+-------------+------------------------+
4 rows in set (0.00 sec)
```





### ORDER BY多列

```
+-------------+------------------------+
| word        | translation            |
+-------------+------------------------+
| creatural   | adj.动物的,人的        |
| shaviana    | [复]n.有关萧伯纳的文物 |
| xylographer | n.木刻师,刻版师        |
| redo        | v.再做 重做            |
+-------------+------------------------+
4 rows in set (0.00 sec)


mysql> SELECT * FROM review_table ORDER BY word, translation;
+-------------+------------------------+
| word        | translation            |
+-------------+------------------------+
| creatural   | adj.动物的,人的        |
| redo        | v.再做 重做            |
| shaviana    | [复]n.有关萧伯纳的文物 |
| xylographer | n.木刻师,刻版师        |
+-------------+------------------------+
4 rows in set (0.00 sec)
```





## SQL INSERT INTO 语句

INSERT INTO 语句用于向表中插入新记录。

### SQL INSERT INTO 语法

INSERT INTO 语句可以有两种编写形式。

第一种形式无需指定要插入数据的列名，只需提供被插入的值即可：

```
INSERT INTO table_name
VALUES (value1,value2,value3,...);
```

第二种形式需要指定列名及被插入的值：

```
INSERT INTO table_name (column1,column2,column3,...)
VALUES (value1,value2,value3,...);
```

**参数说明：**

- **table_name**：需要插入新记录的表名。
- **column1, column2, ...**：需要插入的字段名。
- **value1, value2, ...**：需要插入的字段值。

#### 演示数据库

在本教程中，我们将使用 RUNOOB 样本数据库。

下面是选自 "Websites" 表的数据：

```
+----+--------------+---------------------------+-------+---------+
| id | name         | url                       | alexa | country |
+----+--------------+---------------------------+-------+---------+
| 1  | Google       | https://www.google.cm/    | 1     | USA     |
| 2  | 淘宝          | https://www.taobao.com/   | 13    | CN      |
| 3  | 菜鸟教程      | http://www.runoob.com/    | 4689  | CN      |
| 4  | 微博          | http://weibo.com/         | 20    | CN      |
| 5  | Facebook     | https://www.facebook.com/ | 3     | USA     |
+----+--------------+---------------------------+-------+---------+
```

------

### INSERT INTO 实例

假设我们要向 "Websites" 表中插入一个新行。

我们可以使用下面的 SQL 语句：

#### 实例

INSERT INTO Websites (name, url, alexa, country) VALUES ('百度','https://www.baidu.com/','4','CN');

执行以上 SQL，再读取 "Websites" 表，数据如下所示：

![img](https://www.runoob.com/wp-content/uploads/2013/09/insert1.jpg)

##### insert into select 和select into from 的区别

```
insert into scorebak select * from socre where neza='neza'   --插入一行,要求表scorebak 必须存在
select *  into scorebak from score  where neza='neza'  --也是插入一行,要求表scorebak 不存在
```



## SQL UPDATE 语句

UPDATE 语句用于更新表中已存在的记录。

### SQL UPDATE 语法

```
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

参数说明：

- **table_name**：要修改的表名称。
- **column1, column2, ...**：要修改的字段名称，可以为多个字段。
- **value1, value2, ...**：要修改的值，可以为多个值。
- **condition**：修改条件，用于指定哪些数据要修改。

| ![lamp](https://www.runoob.com/images/lamp.jpg) | **请注意 SQL UPDATE 语句中的 WHERE 子句！** WHERE 子句规定哪条记录或者哪些记录需要更新。如果您省略了 WHERE 子句，所有的记录都将被更新！ |
| ----------------------------------------------- | ------------------------------------------------------------ |
|                                                 |                                                              |

实例

使用的数据表：

```
+-------------+------------------------+
| word        | translation            |
+-------------+------------------------+
| creatural   | adj.动物的,人的        |
| redo        | v.再做 重做            |
| shaviana    | [复]n.有关萧伯纳的文物 |
| xylographer | n.木刻师,刻版师        |
+-------------+------------------------+
```

更新过后：

```
mysql> SELECT * FROM review_table;
+-------------+------------------------+
| word        | translation            |
+-------------+------------------------+
| creatural   | adj.动物的,人的        |
| shaviana    | [复]n.有关萧伯纳的文物 |
| xylographer | n.木刻师,刻版师        |
| redo        | HAHA                   |
+-------------+------------------------+
4 rows in set (0.00 sec)
```



#### Update 警告！

在更新记录时要格外小心！在上面的实例中，如果我们省略了 WHERE 子句，如下所示：

```
UPDATE Websites
SET alexa='5000', country='USA'
```

执行以上代码会将 Websites 表中所有数据的 alexa 改为 5000，country 改为 USA。

执行没有 WHERE 子句的 UPDATE 要慎重，再慎重。







## SQL DELETE 语句

DELETE 语句用于删除表中的行。

### SQL DELETE 语法

```
DELETE FROM table_name
WHERE condition;
```

参数说明：

- **table_name**：要删除的表名称。
- **condition**：删除条件，用于指定哪些数据要删除。

| ![lamp](https://www.runoob.com/images/lamp.jpg) | **请注意 SQL DELETE 语句中的 WHERE 子句！** WHERE 子句规定哪条记录或者哪些记录需要删除。如果您省略了 WHERE 子句，所有的记录都将被删除！ |
| ----------------------------------------------- | ------------------------------------------------------------ |
|                                                 |                                                              |

实例：

```
+-------------+------------------------+
| word        | translation            |
+-------------+------------------------+
| creatural   | adj.动物的,人的        |
| redo        | v.再做 重做            |
| shaviana    | [复]n.有关萧伯纳的文物 |
| xylographer | n.木刻师,刻版师        |
+-------------+------------------------+
```

删除过后：

```
mysql> DELETE FROM review_table WHERE word='redo';
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM review_table;
+-------------+------------------------+
| word        | translation            |
+-------------+------------------------+
| creatural   | adj.动物的,人的        |
| shaviana    | [复]n.有关萧伯纳的文物 |
| xylographer | n.木刻师,刻版师        |
+-------------+------------------------+
3 rows in set (0.00 sec)
```



#### 删除所有数据

您可以在不删除表的情况下，删除表中所有的行。这意味着表结构、属性、索引将保持不变：

DELETE FROM *table_name*;

**注释：**在删除记录时要格外小心！因为您不能重来！





## SELECT TOP 子句

SELECT TOP 子句用于规定要返回的记录的数目。

SELECT TOP 子句对于拥有数千条记录的大型表来说，是非常有用的。



### MySQL 语法

```
SELECT column_name(s)
FROM table_name
LIMIT number;
```

限定返回数据条数

实例显示了两行数据，而不是所有数据

```
mysql> SELECT * FROM review_table LIMIT 2;
+-----------+------------------------+
| word      | translation            |
+-----------+------------------------+
| creatural | adj.动物的,人的        |
| shaviana  | [复]n.有关萧伯纳的文物 |
+-----------+------------------------+
2 rows in set (0.00 sec)
```



## SQL SELECT TOP PERCENT 实例

在 Microsoft SQL Server 中还可以使用百分比作为参数。

下面的 SQL 语句从 websites 表中选取前面百分之 50 的记录：



### SQL Server / MS Access 语法

```
SELECT TOP number|percent column_name(s)
FROM table_name;
```

实例

以下操作在 Microsoft SQL Server 数据库中可执行。

```
SELECT TOP 50 PERCENT * FROM Websites;
```





### SQL LIMIT

```
mysql> SELECT * FROM review_table LIMIT 2;
+-----------+------------------------+
| word      | translation            |
+-----------+------------------------+
| creatural | adj.动物的,人的        |
| shaviana  | [复]n.有关萧伯纳的文物 |
+-----------+------------------------+
2 rows in set (0.00 sec)
```





## SQL LIKE 操作符

LIKE 操作符用于在 WHERE 子句中搜索列中的指定模式。

### SQL LIKE 语法

```
SELECT column1, column2, ...
FROM table_name
WHERE column LIKE pattern;
```

参数说明：

- **column1, column2, ...**：要选择的字段名称，可以为多个字段。如果不指定字段名称，则会选择所有字段。
- **table_name**：要查询的表名称。
- **column**：要搜索的字段名称。
- **pattern**：搜索模式			

```
mysql> select * from review_table;
+-------------+------------------------+
| word        | translation            |
+-------------+------------------------+
| creatural   | adj.动物的,人的        |
| shaviana    | [复]n.有关萧伯纳的文物 |
| xylographer | n.木刻师,刻版师        |
+-------------+------------------------+
3 rows in set (0.00 sec)


mysql> select * from review_table where word like "c%";
+-----------+-----------------+
| word      | translation     |
+-----------+-----------------+
| creatural | adj.动物的,人的 |
+-----------+-----------------+
1 row in set (0.00 sec)
```





## SQL 通配符

在 SQL 中，通配符与 SQL LIKE 操作符一起使用。

SQL 通配符用于搜索表中的数据。

在 SQL 中，可使用以下通配符：

| 通配符                         | 描述                   |
| :----------------------------- | :--------------------- |
| %                              | 替代 0 个或多个字符    |
| _                              | 替代一个字符           |
| [*charlist*]                   | 字符列中的任何单一字符 |
| [^*charlist*] 或 [!*charlist*] | 不在字符列中的任何单一 |

[SQL 通配符 | 菜鸟教程 (runoob.com)](https://www.runoob.com/sql/sql-wildcards.html)



### 使用 SQL % 通配符

下面的 SQL 语句选取 url 以字母 "https" 开始的所有网站：

#### 实例

SELECT * FROM Websites
WHERE url LIKE 'https%';

执行输出结果：

![img](https://www.runoob.com/wp-content/uploads/2013/09/wildcards1.jpg)

下面的 SQL 语句选取 url 包含模式 "oo" 的所有网站：

#### 实例

SELECT * FROM Websites
WHERE url LIKE '%oo%';

执行输出结果：

![img](https://www.runoob.com/wp-content/uploads/2013/09/wildcards2.jpg)

------

### 使用 SQL _ 通配符

下面的 SQL 语句选取 name 以一个任意字符开始，然后是 "oogle" 的所有客户：

#### 实例

SELECT * FROM Websites
WHERE name LIKE '_oogle';

执行输出结果：

![img](https://www.runoob.com/wp-content/uploads/2013/09/wildcards3.jpg)

下面的 SQL 语句选取 name 以 "G" 开始，然后是一个任意字符，然后是 "o"，然后是一个任意字符，然后是 "le" 的所有网站：

#### 实例

SELECT * FROM Websites
WHERE name LIKE 'G_o_le';

执行输出结果：

![img](https://www.runoob.com/wp-content/uploads/2013/09/wildcards4.jpg)

------

### 使用 SQL [charlist] 通配符

MySQL 中使用 **REGEXP** 或 **NOT REGEXP** 运算符 (或 RLIKE 和 NOT RLIKE) 来操作正则表达式。

下面的 SQL 语句选取 name 以 "G"、"F" 或 "s" 开始的所有网站：

```
mysql> select * from review_table where word regexp '^[c]\w*';
+-----------+-----------------+
| word      | translation     |
+-----------+-----------------+
| creatural | adj.动物的,人的 |
+-----------+-----------------+
1 row in set (0.00 sec)

mysql> select * from review_table where word regexp '^[c]\w*';
+-----------+-----------------+
| word      | translation     |
+-----------+-----------------+
| creatural | adj.动物的,人的 |
+-----------+-----------------+
1 row in set (0.00 sec)
```







## IN 操作符

IN 操作符允许您在 WHERE 子句中规定多个值。

### SQL IN 语法

```
SELECT column1, column2, ...
FROM table_name
WHERE column IN (value1, value2, ...);
```

参数说明：

- **column1, column2, ...**：要选择的字段名称，可以为多个字段。如果不指定字段名称，则会选择所有字段。
- **table_name**：要查询的表名称。
- **column**：要查询的字段名称。
- **value1, value2, ...**：要查询的值，可以为多个值。

```
mysql> select * from review_table where word in ('creatural');
+-----------+-----------------+
| word      | translation     |
+-----------+-----------------+
| creatural | adj.动物的,人的 |
+-----------+-----------------+
1 row in set (0.00 sec)
```





## SQL BETWEEN 操作符

BETWEEN 操作符选取介于两个值之间的数据范围内的值。这些值可以是数值、文本或者日期。

### SQL BETWEEN 语法

```
SELECT column1, column2, ...
FROM table_name
WHERE column BETWEEN value1 AND value2;
```

参数说明：

- column1, column2, ...：要选择的字段名称，可以为多个字段。如果不指定字段名称，则会选择所有字段。
- table_name：要查询的表名称。
- column：要查询的字段名称。
- value1：范围的起始值。
- value2：范围的结束值。

```
-- 查询review_table表中的列名的开头为a和h之间行数据
mysql> select * from review_table where word between 'a' and 'h';
+-----------+-----------------+
| word      | translation     |
+-----------+-----------------+
| creatural | adj.动物的,人的 |
+-----------+-----------------+
1 row in set (0.00 sec)
```





## SQL 别名

通过使用 SQL，可以为表名称或列名称指定别名。

基本上，创建别名是为了让列名称的可读性更强。

### 列的 SQL 别名语法

```
SELECT column_name AS alias_name
FROM table_name;
```

### 表的 SQL 别名语法

```
SELECT column_name(s)
FROM table_name AS alias_name;
```

------

### 演示数据库

在本教程中，我们将使用 RUNOOB 样本数据库。

下面是选自 "Websites" 表的数据：

```
mysql> SELECT * FROM Websites;
+----+---------------+---------------------------+-------+---------+
| id | name          | url                       | alexa | country |
+----+---------------+---------------------------+-------+---------+
|  1 | Google        | https://www.google.cm/    |     1 | USA     |
|  2 | 淘宝          | https://www.taobao.com/   |    13 | CN      |
|  3 | 菜鸟教程       | http://www.runoob.com/    |  5000 | USA     |
|  4 | 微博           | http://weibo.com/         |    20 | CN      |
|  5 | Facebook      | https://www.facebook.com/ |     3 | USA     |
|  7 | stackoverflow | http://stackoverflow.com/ |     0 | IND     |
+----+---------------+---------------------------+-------+---------+
```

下面是 "access_log" 网站访问记录表的数据：

```
mysql> SELECT * FROM access_log;
+-----+---------+-------+------------+
| aid | site_id | count | date       |
+-----+---------+-------+------------+
|   1 |       1 |    45 | 2016-05-10 |
|   2 |       3 |   100 | 2016-05-13 |
|   3 |       1 |   230 | 2016-05-14 |
|   4 |       2 |    10 | 2016-05-14 |
|   5 |       5 |   205 | 2016-05-14 |
|   6 |       4 |    13 | 2016-05-15 |
|   7 |       3 |   220 | 2016-05-15 |
|   8 |       5 |   545 | 2016-05-16 |
|   9 |       3 |   201 | 2016-05-17 |
+-----+---------+-------+------------+
9 rows in set (0.00 sec)
```

------

### 列的别名实例

下面的 SQL 语句指定了两个别名，一个是 name 列的别名，一个是 country 列的别名。**提示：**如果列名称包含空格，要求使用双引号或方括号：

##### 实例

```
SELECT name AS n, country AS c
FROM Websites;
```

执行输出结果：

![img](https://www.runoob.com/wp-content/uploads/2013/09/alias1.jpg)

在下面的 SQL 语句中，我们把三个列（url、alexa 和 country）结合在一起，并创建一个名为 "site_info" 的别名：

##### 实例

```
SELECT name, CONCAT(url, ', ', alexa, ', ', country) AS site_info
FROM Websites;
```

执行输出结果：

![img](https://www.runoob.com/wp-content/uploads/2013/09/alias2.jpg)

------

### 表的别名实例

下面的 SQL 语句选取 "菜鸟教程" 的所有访问记录。我们使用 "Websites" 和 "access_log" 表，并分别为它们指定表别名 "w" 和 "a"（通过使用别名让 SQL 更简短）：

##### 实例

```
SELECT w.name, w.url, a.count, a.date
FROM Websites AS w, access_log AS a
WHERE a.site_id=w.id and w.name="菜鸟教程";
```

执行输出结果：

![img](https://www.runoob.com/wp-content/uploads/2013/09/alias3.jpg)

不带别名的相同的 SQL 语句：

##### 实例

```
SELECT Websites.name, Websites.url, access_log.count, access_log.date
FROM Websites, access_log
WHERE Websites.id=access_log.site_id and Websites.name="菜鸟教程";
```

执行输出结果：

![img](https://www.runoob.com/wp-content/uploads/2013/09/alias4.jpg)

在下面的情况下，使用别名很有用：

- 在查询中涉及超过一个表
- 在查询中使用了函数
- 列名称很长或者可读性差
- 需要把两个列或者多个列结合在一起





## 连接(JOIN)

------

SQL join 用于把来自两个或多个表的行结合起来。

下图展示了 LEFT JOIN、RIGHT JOIN、INNER JOIN、OUTER JOIN 相关的 7 种用法。

[![img](https://www.runoob.com/wp-content/uploads/2019/01/sql-join.png)](https://www.runoob.com/wp-content/uploads/2019/01/sql-join.png)

------

### SQL JOIN

SQL JOIN 子句用于把来自两个或多个表的行结合起来，基于这些表之间的共同字段。

最常见的 JOIN 类型：**SQL INNER JOIN（简单的 JOIN）**。 SQL INNER JOIN 从多个表中返回满足 JOIN 条件的所有行。

语法：

```
SELECT column1, column2, ...
FROM table1
JOIN table2 ON condition;
```

**参数说明：**

- **column1, column2, ...**：要选择的字段名称，可以为多个字段。如果不指定字段名称，则会选择所有字段。
- **table1**：要连接的第一个表。
- **table2**：要连接的第二个表。
- **condition**：连接条件，用于指定连接方式。

```
-- 从review_table和enwords这两个表中都有的数据查询这两个表中相同翻译的单词

mysql> select review_table.word, review_table.translation, enwords.word, enwords.translation
    -> from review_table inner join enwords on review_table.word=enwords.word;
+-------------+------------------------+-------------+------------------------+
| word        | translation            | word        | translation            |
+-------------+------------------------+-------------+------------------------+
| creatural   | adj.动物的,人的        | creatural   | adj.动物的,人的        |
| shaviana    | [复]n.有关萧伯纳的文物 | shaviana    | [复]n.有关萧伯纳的文物 |
| xylographer | n.木刻师,刻版师        | xylographer | n.木刻师,刻版师        |
+-------------+------------------------+-------------+------------------------+
3 rows in set (0.07 sec)


mysql> select review_table.word, enwords.word
    -> from review_table inner join enwords on review_table.translation=enwords.translation;
+-------------+-------------+
| word        | word        |
+-------------+-------------+
| creatural   | creatural   |
| shaviana    | shaviana    |
| xylographer | xylographer |
+-------------+-------------+
3 rows in set (0.07 sec)
```

### 不同的 SQL JOIN

在我们继续讲解实例之前，我们先列出您可以使用的不同的 SQL JOIN 类型：

- **INNER JOIN**：如果表中有至少一个匹配，则返回行
- **LEFT JOIN**：即使右表中没有匹配，也从左表返回所有的行
- **RIGHT JOIN**：即使左表中没有匹配，也从右表返回所有的行
- **FULL JOIN**：只要其中一个表中存在匹配，则返回行



### SQL INNER JOIN 关键字

INNER JOIN 关键字在表中存在至少一个匹配时返回行。

#### SQL INNER JOIN 语法

>SELECT *column_name(s)*
>FROM *table1*
>INNER JOIN *table2*
>ON *table1.column_name*=*table2.column_name*;

或：

>SELECT *column_name(s)*
>FROM *table1*
>JOIN *table2*
>ON *table1.column_name*=*table2.column_name*;

**参数说明：**

- columns：要显示的列名。
- table1：表1的名称。
- table2：表2的名称。
- column_name：表中用于连接的列名。

**注释：**INNER JOIN 与 JOIN 是相同的。

![SQL INNER JOIN](https://www.runoob.com/wp-content/uploads/2013/09/img_innerjoin.gif)



### SQL LEFT JOIN 关键字

LEFT JOIN 关键字从左表（table1）返回所有的行，即使右表（table2）中没有匹配。如果右表中没有匹配，则结果为 NULL。

#### SQL LEFT JOIN 语法

>SELECT *column_name(s)*
>FROM *table1*
>LEFT JOIN *table2*
>ON *table1.column_name*=*table2.column_name*;

或：

> SELECT *column_name(s)*
> FROM *table1*
> LEFT OUTER JOIN *table2*
> ON *table1.column_name*=*table2.column_name*;

**注释：**在某些数据库中，LEFT JOIN 称为 LEFT OUTER JOIN。

![SQL LEFT JOIN](https://www.runoob.com/wp-content/uploads/2013/09/img_leftjoin.gif)

> mysql> select review_table.word as r_word, enwords.translation as e_trans
>     -> from enwords left join review_table on enwords.word=review_table.word limit 5;
> +--------+--------------------------------------------------------------------------------------------------+
> | r_word | e_trans                                                                                          |
> +--------+--------------------------------------------------------------------------------------------------+
> | NULL   | n.(A)As 或 A's  安(ampere);(a) art.一;n.字母A /[军] Analog.Digital,模拟/数字 /(=account of) 帐上 |
> | NULL   | American Academy of Arts and Letters 美国艺术和文学学会                                          |
> | NULL   |  亚琛[德意志联邦共和国西部城市]                                                                  |
> | NULL   | Airways and Air Communications Service (美国)航路与航空通讯联络处                                |
> | NULL   |  [军]Armored Artillery Howitzer,装甲榴弹炮;[军]Advanced Attack Helicopter,先进攻击直升机         |
> +--------+--------------------------------------------------------------------------------------------------+
> 5 rows in set (0.00 sec)

 这里由于是左包含所以会不管review_table与enwords有没有交集，都将review_table的数据查询出来，但是因为limit 5 所以限制查询5条，而review_table与enwords有交集的部分不在前5条中，所以r_word一列中的内容为NULL



### SQL RIGHT JOIN 关键字

RIGHT JOIN 关键字从右表（table2）返回所有的行，即使左表（table1）中没有匹配。如果左表中没有匹配，则结果为 NULL。

#### SQL RIGHT JOIN 语法

SELECT *column_name(s)*
FROM *table1*
RIGHT JOIN *table2*
ON *table1.column_name*=*table2.column_name*;

或：

SELECT *column_name(s)*
FROM *table1*
RIGHT OUTER JOIN *table2*
ON *table1.column_name*=*table2.column_name*;

**注释：**在某些数据库中，RIGHT JOIN 称为 RIGHT OUTER JOIN。

![SQL RIGHT JOIN](https://www.runoob.com/wp-content/uploads/2013/09/img_rightjoin.gif)





### SQL FULL OUTER JOIN 关键字

FULL OUTER JOIN 关键字只要左表（table1）和右表（table2）其中一个表中存在匹配，则返回行.

FULL OUTER JOIN 关键字结合了 LEFT JOIN 和 RIGHT JOIN 的结果。

#### SQL FULL OUTER JOIN 语法

SELECT *column_name(s)*
FROM *table1*
FULL OUTER JOIN *table2*
ON *table1.column_name*=*table2.column_name*;

![SQL FULL OUTER JOIN](https://www.runoob.com/wp-content/uploads/2013/09/img_fulljoin.gif)



### SQL UNION 操作符

UNION 操作符用于合并两个或多个 SELECT 语句的结果集。

请注意，UNION 内部的每个 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每个 SELECT 语句中的列的顺序必须相同。

#### SQL UNION 语法

```
SELECT *column_name(s)* FROM *table1*
UNION
SELECT *column_name(s)* FROM *table2*;
```

**注释：**默认地，UNION 操作符选取不同的值。如果允许重复的值，请使用 UNION ALL。

#### SQL UNION ALL 语法

```
SELECT *column_name(s)* FROM *table1*
UNION ALL
SELECT *column_name(s)* FROM *table2*;
```

**注释：**UNION 结果集中的列名总是等于 UNION 中第一个 SELECT 语句中的列名。

> mysql> select * from review_table
>     -> union
>     -> select * from enwords limit 7;
>    
> +-------------+--------------------------------------------------------------------------------------------------+
> | word        | translation                                                                                      |
> +-------------+--------------------------------------------------------------------------------------------------+
> | creatural   | adj.动物的,人的                                                                                  |
> | shaviana    | [复]n.有关萧伯纳的文物                                                                           |
> | xylographer | n.木刻师,刻版师                                                                                  |
> | a           | n.(A)As 或 A's  安(ampere);(a) art.一;n.字母A /[军] Analog.Digital,模拟/数字 /(=account of) 帐上 |
> | aaal        | American Academy of Arts and Letters 美国艺术和文学学会                                          |
> | aachen      |  亚琛[德意志联邦共和国西部城市]                                                                  |
> | aacs        | Airways and Air Communications Service (美国)航路与航空通讯联络处                                |
> +-------------+--------------------------------------------------------------------------------------------------+
> 7 rows in set (0.00 sec)



### 带有 WHERE 的 SQL UNION ALL

下面的 SQL 语句使用 UNION ALL 从 "Websites" 和 "apps" 表中选取**所有的**中国(CN)的数据（也有重复的值）：

> mysql> select * from review_table
>     -> union all
>     -> select * from enwords where word in ('a', 'aaal', 'aachen') order by word;
>    
> +-------------+--------------------------------------------------------------------------------------------------+
> | word        | translation                                                                                      |
> +-------------+--------------------------------------------------------------------------------------------------+
> | a           | n.(A)As 或 A's  安(ampere);(a) art.一;n.字母A /[军] Analog.Digital,模拟/数字 /(=account of) 帐上 |
> | aaal        | American Academy of Arts and Letters 美国艺术和文学学会                                          |
> | aachen      |  亚琛[德意志联邦共和国西部城市]                                                                  |
> | creatural   | adj.动物的,人的                                                                                  |
> | shaviana    | [复]n.有关萧伯纳的文物                                                                           |
> | xylographer | n.木刻师,刻版师                                                                                  |
> +-------------+--------------------------------------------------------------------------------------------------+
> 6 rows in set (0.00 sec)



## SQL SELECT INTO 语句

SELECT INTO 语句从一个表复制数据，然后把数据插入到另一个新表中。

> **注意：**
>
> MySQL 数据库不支持 SELECT ... INTO 语句，但支持 [INSERT INTO ... SELECT](https://www.runoob.com/sql/sql-insert-into-select.html) 。
>
> 当然你可以使用以下语句来拷贝表结构及数据：
>
> ```
> CREATE TABLE 新表
> AS
> SELECT * FROM 旧表 
> ```

### SQL SELECT INTO 语法

我们可以复制所有的列插入到新表中：

```
SELECT *
INTO *newtable* [IN *externaldb*]
FROM *table1;*
```

或者只复制希望的列插入到新表中：

```
SELECT *column_name(s)*
INTO *newtable* [IN *externaldb*]
FROM *table1;
```



| ![lamp](https://www.runoob.com/images/lamp.jpg) | **提示：**新表将会使用 SELECT 语句中定义的列名称和类型进行创建。您可以使用 AS 子句来应用新名称。 |
| ----------------------------------------------- | ------------------------------------------------------------ |
|                                                 |                                                              |

`注意：select into 在mysql数据库中是不支持的，但我们可以使用`

`insert into new_table select columns from old_table  where ...`

来实现以上的功能

实例：

> mysql> insert into review_table select * from enwords where word in ('a', 'aaal', 'aachen') limit 5;
> Query OK, 3 rows affected (0.01 sec)
> Records: 3  Duplicates: 0  Warnings: 0

> mysql> select * from review_table;
> +-------------+--------------------------------------------------------------------------------------------------+
> | word        | translation                                                                                      |
> +-------------+--------------------------------------------------------------------------------------------------+
> | creatural   | adj.动物的,人的                                                                                  |
> | shaviana    | [复]n.有关萧伯纳的文物                                                                           |
> | xylographer | n.木刻师,刻版师                                                                                  |
> | a           | n.(A)As 或 A's  安(ampere);(a) art.一;n.字母A /[军] Analog.Digital,模拟/数字 /(=account of) 帐上 |
> | aaal        | American Academy of Arts and Letters 美国艺术和文学学会                                          |
> | aachen      |  亚琛[德意志联邦共和国西部城市]                                                                  |
> +-------------+--------------------------------------------------------------------------------------------------+
> 6 rows in set (0.00 sec)







## SQL INSERT INTO SELECT 语句

INSERT INTO SELECT 语句从一个表复制数据，然后把数据插入到一个已存在的表中。目标表中任何已存在的行都不会受影响。

### SQL INSERT INTO SELECT 语法

我们可以从一个表中复制所有的列插入到另一个已存在的表中：

```
**INSERT** **INTO** table2
**SELECT** * **FROM** table1;
```

或者我们可以只复制指定的列插入到另一个已存在的表中：



```
**INSERT** **INTO** table2
(column_name(s))
**SELECT** column_name(s)
**FROM** table1;
```

实例：

mysql> insert into review_table select * from enwords where word in ('a', 'aaal', 'aachen') limit 5;
Query OK, 3 rows affected (0.01 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> select * from review_table;

> +-------------+--------------------------------------------------------------------------------------------------+
> | word        | translation                                                                                      |
> +-------------+--------------------------------------------------------------------------------------------------+
> | creatural   | adj.动物的,人的                                                                                  |
> | shaviana    | [复]n.有关萧伯纳的文物                                                                           |
> | xylographer | n.木刻师,刻版师                                                                                  |
> | a           | n.(A)As 或 A's  安(ampere);(a) art.一;n.字母A /[军] Analog.Digital,模拟/数字 /(=account of) 帐上 |
> | aaal        | American Academy of Arts and Letters 美国艺术和文学学会                                          |
> | aachen      |  亚琛[德意志联邦共和国西部城市]                                                                  |
> +-------------+--------------------------------------------------------------------------------------------------+
> 6 rows in set (0.00 sec)

> mysql> select * from review_table;
> +-------------+--------------------------------------------------------------------------------------------------+
> | word        | translation                                                                                      |
> +-------------+--------------------------------------------------------------------------------------------------+
> | creatural   | adj.动物的,人的                                                                                  |
> | shaviana    | [复]n.有关萧伯纳的文物                                                                           |
> | xylographer | n.木刻师,刻版师                                                                                  |
> | a           | n.(A)As 或 A's  安(ampere);(a) art.一;n.字母A /[军] Analog.Digital,模拟/数字 /(=account of) 帐上 |
> | aaal        | American Academy of Arts and Letters 美国艺术和文学学会                                          |
> | aachen      |  亚琛[德意志联邦共和国西部城市]                                                                  |
> +-------------+--------------------------------------------------------------------------------------------------+
> 6 rows in set (0.00 sec)





## SQL CREATE DATABASE 语句

CREATE DATABASE 语句用于创建数据库。	

### SQL CREATE DATABASE 语法

CREATE DATABASE *dbname*;

------

### SQL CREATE DATABASE 实例

下面的 SQL 语句创建一个名为 "my_db" 的数据库：

CREATE DATABASE my_db;

数据库表可以通过 CREATE TABLE 语句来添加。









## SQL CREATE TABLE 语句

CREATE TABLE 语句用于创建数据库中的表。

表由行和列组成，每个表都必须有个表名。

### SQL CREATE TABLE 语法

> CREATE TABLE *table_name*
> (
> *column_name1 data_type*(*size*),
> *column_name2 data_type*(*size*),
> *column_name3 data_type*(*size*),
> ....
> );

column_name 参数规定表中列的名称。

data_type 参数规定列的数据类型（例如 varchar、integer、decimal、date 等等）。

size 参数规定表中列的最大长度。

**提示：**如需了解 MS Access、MySQL 和 SQL Server 中可用的数据类型，请访问我们完整的 [数据类型参考手册](https://www.runoob.com/sql/sql-datatypes.html)。

------

#### SQL CREATE TABLE 实例

现在我们想要创建一个名为 "Persons" 的表，包含五列：PersonID、LastName、FirstName、Address 和 City。

我们使用下面的 CREATE TABLE 语句：

```
CREATE TABLE Persons
(
PersonID int,
LastName varchar(255),
FirstName varchar(255),
Address varchar(255),
City varchar(255)
);
```

PersonID 列的数据类型是 int，包含整数。

LastName、FirstName、Address 和 City 列的数据类型是 varchar，包含字符，且这些字段的最大长度为 255 个字符。

空的 "Persons" 表如下所示：

| PersonID | LastName | FirstName | Address | City |
| :------- | :------- | :-------- | :------ | :--- |
|          |          |           |         |      |

**提示：**可使用 INSERT INTO 语句向空表写入数据。



## SQL 约束（Constraints）

SQL 约束用于规定表中的数据规则。

如果存在违反约束的数据行为，行为会被约束终止。

约束可以在创建表时规定（通过 CREATE TABLE 语句），或者在表创建之后规定（通过 ALTER TABLE 语句）。

### SQL CREATE TABLE + CONSTRAINT 语法

> CREATE TABLE *table_name*
> (
> *column_name1 data_type*(*size*) *constraint_name*,
> *column_name2 data_type*(*size*) *constraint_name*,
> *column_name3 data_type*(*size*) *constraint_name*,
> ....
> );

在 SQL 中，我们有如下约束：

- **NOT NULL** - 指示某列不能存储 NULL 值。
- **UNIQUE** - 保证某列的每行必须有唯一的值。
- **PRIMARY KEY** - NOT NULL 和 UNIQUE 的结合。确保某列（或两个列多个列的结合）有唯一标识，有助于更容易更快速地找到表中的一个特定的记录。
- **FOREIGN KEY** - 保证一个表中的数据匹配另一个表中的值的参照完整性。
- **CHECK** - 保证列中的值符合指定的条件。
- **DEFAULT** - 规定没有给列赋值时的默认值。





## SQL NOT NULL 约束

NOT NULL 约束强制列不接受 NULL 值。

NOT NULL 约束强制字段始终包含值。这意味着，如果不向字段添加值，就无法插入新记录或者更新记录。

下面的 SQL 强制 "ID" 列、 "LastName" 列以及 "FirstName" 列不接受 NULL 值：

```
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);
```



### 添加 NOT NULL 约束

在一个已创建的表的 "Age" 字段中添加 NOT NULL 约束如下所示：

```
mysql> alter table review_table
    -> modify word varchar(300) not null;
Query OK, 0 rows affected (0.05 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc review_table;
+-------------+--------------+------+-----+---------+-------+
| Field       | Type         | Null | Key | Default | Extra |
+-------------+--------------+------+-----+---------+-------+
| word        | varchar(300) | NO   |     | NULL    |       |
| translation | varchar(300) | YES  |     | NULL    |       |
+-------------+--------------+------+-----+---------+-------+
2 rows in set (0.01 sec)
```



### 删除 NOT NULL 约束

在一个已创建的表的 "Age" 字段中删除 NOT NULL 约束如下所示：

```
mysql> alter table review_table
    -> modify word varchar(300) null;
Query OK, 0 rows affected (0.03 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc review_table;
+-------------+--------------+------+-----+---------+-------+
| Field       | Type         | Null | Key | Default | Extra |
+-------------+--------------+------+-----+---------+-------+
| word        | varchar(300) | YES  |     | NULL    |       |
| translation | varchar(300) | YES  |     | NULL    |       |
+-------------+--------------+------+-----+---------+-------+
2 rows in set (0.00 sec)
```





## SQL UNIQUE 约束

UNIQUE 约束唯一标识数据库表中的每条记录。

UNIQUE 和 PRIMARY KEY 约束均为列或列集合提供了唯一性的保证。

PRIMARY KEY 约束拥有自动定义的 UNIQUE 约束。

请注意，每个表可以有多个 UNIQUE 约束，但是每个表只能有一个 PRIMARY KEY 约束。

------

### CREATE TABLE 时的 SQL UNIQUE 约束

下面的 SQL 在 "Persons" 表创建时在 "P_Id" 列上创建 UNIQUE 约束：

**MySQL：**

```
CREATE TABLE Persons
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
UNIQUE (P_Id)
)
```

### ALTER TABLE 时的 SQL UNIQUE 约束

当表已被创建时，如需在 "P_Id" 列创建 UNIQUE 约束，请使用下面的 SQL：

**MySQL / SQL Server / Oracle / MS Access：**

> ALTER TABLE Persons
> ADD UNIQUE (P_Id)

如需命名 UNIQUE 约束，并定义多个列的 UNIQUE 约束，请使用下面的 SQL 语法：

**MySQL / SQL Server / Oracle / MS Access：**

> ALTER TABLE Persons
> ADD CONSTRAINT uc_PersonID UNIQUE (P_Id,LastName)

------

`这里的ADD constraint 约束名 约束（unique）要约束的列，指的是为表的某个列添加有约束名的约束`



### 撤销 UNIQUE 约束

如需撤销 UNIQUE 约束，请使用下面的 SQL：

**MySQL：**

> ALTER TABLE Persons
> DROP INDEX uc_PersonID   （删除约束）

**SQL Server / Oracle / MS Access：**

> ALTER TABLE Persons
> DROP CONSTRAINT uc_PersonID  (删除指定约束名的约束)

实例：

>mysql> alter table enwords add constraint uqe unique (word);
>Query OK, 0 rows affected (0.27 sec)
>Records: 0  Duplicates: 0  Warnings: 0

> mysql> desc enwords;
> +-------------+--------------+------+-----+---------+-------+
> | Field       | Type         | Null | Key | Default | Extra |
> +-------------+--------------+------+-----+---------+-------+
> | word        | varchar(32)  | NO   | PRI |         |       |
> | translation | varchar(512) | YES  |     | NULL    |       |
> +-------------+--------------+------+-----+---------+-------+
> 2 rows in set (0.00 sec)



> mysql> alter table review_table add unique (word);
> Query OK, 0 rows affected (0.03 sec)
> Records: 0  Duplicates: 0  Warnings: 0

>mysql> desc review_table;
>+-------------+--------------+------+-----+---------+-------+
>| Field       | Type         | Null | Key | Default | Extra |
>+-------------+--------------+------+-----+---------+-------+
>| word        | varchar(300) | YES  | UNI | NULL    |       |
>| translation | varchar(300) | YES  |     | NULL    |       |
>+-------------+--------------+------+-----+---------+-------+
>2 rows in set (0.00 sec)





## SQL PRIMARY KEY 约束

PRIMARY KEY 约束唯一标识数据库表中的每条记录。

主键必须包含唯一的值。

主键列不能包含 NULL 值。

每个表都应该有一个主键，并且每个表只能有一个主键。

------

### CREATE TABLE 时的 SQL PRIMARY KEY 约束

下面的 SQL 在 "Persons" 表创建时在 "P_Id" 列上创建 PRIMARY KEY 约束：

**MySQL：**

> CREATE TABLE Persons
> (
> P_Id int NOT NULL,
> LastName varchar(255) NOT NULL,
> FirstName varchar(255),
> Address varchar(255),
> City varchar(255),
> PRIMARY KEY (P_Id)
> )

`注意:创建主键的时候，需要先创建出要设置为主键的列，并且需要将该列设置为not null`

### ALTER TABLE 时的 SQL PRIMARY KEY 约束

当表已被创建时，如需在 "P_Id" 列创建 PRIMARY KEY 约束，请使用下面的 SQL：

**MySQL / SQL Server / Oracle / MS Access：**

> ALTER TABLE Persons
> ADD PRIMARY KEY (P_Id)

如需命名 PRIMARY KEY 约束，并定义多个列的 PRIMARY KEY 约束，请使用下面的 SQL 语法：

**MySQL / SQL Server / Oracle / MS Access：**

> ALTER TABLE Persons
> ADD CONSTRAINT pk_PersonID PRIMARY KEY (P_Id,LastName)

**注释：**如果您使用 ALTER TABLE 语句添加主键，必须把主键列声明为不包含 NULL 值（在表首次创建时）。

实例：

>mysql> alter table enwords  drop primary key;
>Query OK, 103976 rows affected (0.81 sec)
>Records: 103976  Duplicates: 0  Warnings: 0

>mysql> alter table enwords add primary key (word);
>Query OK, 0 rows affected (0.37 sec)
>Records: 0  Duplicates: 0  Warnings: 0

>mysql> desc enwords;
>+-------------+--------------+------+-----+---------+-------+
>| Field       | Type         | Null | Key | Default | Extra |
>+-------------+--------------+------+-----+---------+-------+
>| word        | varchar(32)  | NO   | PRI |         |       |
>| translation | varchar(512) | YES  |     | NULL    |       |
>+-------------+--------------+------+-----+---------+-------+
>2 rows in set (0.00 sec)



### 撤销 PRIMARY KEY 约束

如需撤销 PRIMARY KEY 约束，请使用下面的 SQL：

**MySQL：**

> ALTER TABLE Persons
> DROP PRIMARY KEY

**SQL Server / Oracle / MS Access：**

> ALTER TABLE Persons
> DROP CONSTRAINT pk_PersonID

实例

> mysql> alter table enwords  drop primary key;
> Query OK, 103976 rows affected (0.81 sec)
> Records: 103976  Duplicates: 0  Warnings: 0



----



## SQL FOREIGN KEY 约束

一个表中的 FOREIGN KEY 指向另一个表中的 UNIQUE KEY(唯一约束的键)。

让我们通过一个实例来解释外键。请看下面两个表：

"Persons" 表：

| P_Id | LastName  | FirstName | Address      | City      |
| :--- | :-------- | :-------- | :----------- | :-------- |
| 1    | Hansen    | Ola       | Timoteivn 10 | Sandnes   |
| 2    | Svendson  | Tove      | Borgvn 23    | Sandnes   |
| 3    | Pettersen | Kari      | Storgt 20    | Stavanger |

"Orders" 表：

| O_Id | OrderNo | P_Id |
| :--- | :------ | :--- |
| 1    | 77895   | 3    |
| 2    | 44678   | 3    |
| 3    | 22456   | 2    |
| 4    | 24562   | 1    |

请注意，"Orders" 表中的 "P_Id" 列指向 "Persons" 表中的 "P_Id" 列。

"Persons" 表中的 "P_Id" 列是 "Persons" 表中的 PRIMARY KEY。

"Orders" 表中的 "P_Id" 列是 "Orders" 表中的 FOREIGN KEY。

FOREIGN KEY 约束用于预防破坏表之间连接的行为。

FOREIGN KEY 约束也能防止非法数据插入外键列，因为它必须是它指向的那个表中的值之一。



### CREATE TABLE 时的 SQL FOREIGN KEY 约束

下面的 SQL 在 "Orders" 表创建时在 "P_Id" 列上创建 FOREIGN KEY 约束：

**MySQL：**

> CREATE TABLE Orders
> (
> O_Id int NOT NULL,
> OrderNo int NOT NULL,
> P_Id int,
> PRIMARY KEY (O_Id),
> FOREIGN KEY (P_Id) REFERENCES Persons(P_Id)
> )

`注意:创建外键的时候，需要先创建出要设置为外键的列，并且需要指向对应的表的主键`

**SQL Server / Oracle / MS Access：**

> CREATE TABLE Orders
> (
> O_Id int NOT NULL PRIMARY KEY,
> OrderNo int NOT NULL,
> P_Id int FOREIGN KEY REFERENCES Persons(P_Id)
> )

如需命名 FOREIGN KEY 约束，并定义多个列的 FOREIGN KEY 约束，请使用下面的 SQL 语法：

**MySQL / SQL Server / Oracle / MS Access：**

> CREATE TABLE Orders
> (
> O_Id int NOT NULL,
> OrderNo int NOT NULL,
> P_Id int,
> PRIMARY KEY (O_Id),
> CONSTRAINT fk_PerOrders FOREIGN KEY (P_Id)
> REFERENCES Persons(P_Id)
> )





### ALTER TABLE 时的 SQL FOREIGN KEY 约束

当 "Orders" 表已被创建时，如需在 "P_Id" 列创建 FOREIGN KEY 约束，请使用下面的 SQL：

**MySQL / SQL Server / Oracle / MS Access：**

> ALTER TABLE Orders
> ADD FOREIGN KEY (P_Id)
> REFERENCES Persons(P_Id)

如需命名 FOREIGN KEY 约束，并定义多个列的 FOREIGN KEY 约束，请使用下面的 SQL 语法：

**MySQL / SQL Server / Oracle / MS Access：**

> ALTER TABLE Orders
> ADD CONSTRAINT fk_PerOrders
> FOREIGN KEY (P_Id)
> REFERENCES Persons(P_Id)

------

### 撤销 FOREIGN KEY 约束

如需撤销 FOREIGN KEY 约束，请使用下面的 SQL：

**MySQL：**

> ALTER TABLE Orders
> DROP FOREIGN KEY fk_PerOrders

**SQL Server / Oracle / MS Access：**

> ALTER TABLE Orders
> DROP CONSTRAINT fk_PerOrders



`注意：`

删除外键需要知道外键的名称，如果创建时没有设置名称则会自动生成一个，你需要获取改外键的信息。

使用以下命令获取外键信息：

```
SELECT
  constraint_name
FROM
  information_schema.REFERENTIAL_CONSTRAINTS
WHERE
  constraint_schema = <'db_name'> AND table_name = <'table_name'>;
  
SELECT *
FROM
  information_schema.KEY_COLUMN_USAGE
WHERE
  constraint_schema = <'db_name'> AND table_name = <'table_name'> AND   
  referenced_table_name IS NOT NULL;
```

可以使用以下命令来删除外键：

```
ALTER TABLE <table_name> DROP INDEX <fk_name>;
```



## SQL CHECK 约束

CHECK 约束用于限制列中的值的范围。

如果对单个列定义 CHECK 约束，那么该列只允许特定的值。

如果对一个表定义 CHECK 约束，那么此约束会基于行中其他列的值在特定的列中对值进行限制。



### CREATE TABLE 时的 SQL CHECK 约束

下面的 SQL 在 "Persons" 表创建时在 "P_Id" 列上创建 CHECK 约束。CHECK 约束规定 "P_Id" 列必须只包含大于 0 的整数。

**MySQL：**

> CREATE TABLE Persons
> (
> P_Id int NOT NULL,
> LastName varchar(255) NOT NULL,
> FirstName varchar(255),
> Address varchar(255),
> City varchar(255),
> CHECK (P_Id>0)
> )

**SQL Server / Oracle / MS Access：**

> CREATE TABLE Persons
> (
> P_Id int NOT NULL CHECK (P_Id>0),
> LastName varchar(255) NOT NULL,
> FirstName varchar(255),
> Address varchar(255),
> City varchar(255)
> )

如需命名 CHECK 约束，并定义多个列的 CHECK 约束，请使用下面的 SQL 语法：

**MySQL / SQL Server / Oracle / MS Access：**

> CREATE TABLE Persons
> (
> P_Id int NOT NULL,
> LastName varchar(255) NOT NULL,
> FirstName varchar(255),
> Address varchar(255),
> City varchar(255),
> CONSTRAINT chk_Person CHECK (P_Id>0 AND City='Sandnes')
> )

------

### ALTER TABLE 时的 SQL CHECK 约束

当表已被创建时，如需在 "P_Id" 列创建 CHECK 约束，请使用下面的 SQL：

**MySQL / SQL Server / Oracle / MS Access:**

> ALTER TABLE Persons
> ADD CHECK (P_Id>0)

如需命名 CHECK 约束，并定义多个列的 CHECK 约束，请使用下面的 SQL 语法：

**MySQL / SQL Server / Oracle / MS Access：**

> ALTER TABLE Persons
> ADD CONSTRAINT chk_Person CHECK (P_Id>0 AND City='Sandnes')

------

### 撤销 CHECK 约束

如需撤销 CHECK 约束，请使用下面的 SQL：

**SQL Server / Oracle / MS Access：**

> ALTER TABLE Persons
> DROP CONSTRAINT chk_Person

**MySQL：**

> ALTER TABLE Persons
> DROP CHECK chk_Person





## SQL DEFAULT 约束

DEFAULT 约束用于向列中插入默认值。

如果没有规定其他的值，那么会将默认值添加到所有的新记录。

------

### CREATE TABLE 时的 SQL DEFAULT 约束

下面的 SQL 在 "Persons" 表创建时在 "City" 列上创建 DEFAULT 约束：

**My SQL / SQL Server / Oracle / MS Access：**

```
CREATE TABLE Persons
(
    P_Id int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255) DEFAULT 'Sandnes'
)
```

通过使用类似 GETDATE() 这样的函数，DEFAULT 约束也可以用于插入系统值：

```
CREATE TABLE Orders
(
    O_Id int NOT NULL,
    OrderNo int NOT NULL,
    P_Id int,
    OrderDate date DEFAULT GETDATE()
)
```

------

### ALTER TABLE 时的 SQL DEFAULT 约束

当表已被创建时，如需在 "City" 列创建 DEFAULT 约束，请使用下面的 SQL：

**MySQL：**

```
ALTER TABLE Persons
ALTER City SET DEFAULT 'SANDNES'
```

**SQL Server / MS Access：**

```
ALTER TABLE Persons
ADD CONSTRAINT ab_c DEFAULT 'SANDNES' for City
```

**Oracle：**

```
ALTER TABLE Persons
MODIFY City DEFAULT 'SANDNES'
```

------

### 撤销 DEFAULT 约束

如需撤销 DEFAULT 约束，请使用下面的 SQL：

**MySQL：**

```
ALTER TABLE Persons
ALTER City DROP DEFAULT
```

**SQL Server / Oracle / MS Access：**

```
ALTER TABLE Persons
ALTER COLUMN City DROP DEFAULT
```







## CREATE INDEX 语句

------

CREATE INDEX 语句用于在表中创建索引。

在不读取整个表的情况下，索引使数据库应用程序可以更快地查找数据。

------

### 索引

您可以在表中创建索引，以便更加快速高效地查询数据。

用户无法看到索引，它们只能被用来加速搜索/查询。

**注释：**更新一个包含索引的表需要比更新一个没有索引的表花费更多的时间，这是由于索引本身也需要更新。因此，理想的做法是仅仅在常常被搜索的列（以及表）上面创建索引。

### SQL CREATE INDEX 语法

在表上创建一个简单的索引。允许使用重复的值：

> CREATE INDEX index_name
> ON table_name (column_name)

### SQL CREATE UNIQUE INDEX 语法

在表上创建一个唯一的索引。不允许使用重复的值：唯一的索引意味着两个行不能拥有相同的索引值。Creates a unique index on a table. Duplicate values are not allowed:

> CREATE UNIQUE INDEX index_name
> ON table_name (column_name)

**注释：**用于创建索引的语法在不同的数据库中不一样。因此，检查您的数据库中创建索引的语法。

------

##### CREATE INDEX 实例

下面的 SQL 语句在 "Persons" 表的 "LastName" 列上创建一个名为 "PIndex" 的索引：

> CREATE INDEX PIndex
> ON Persons (LastName)

如果您希望索引不止一个列，您可以在括号中列出这些列的名称，用逗号隔开：

> CREATE INDEX PIndex
> ON Persons (LastName, FirstName)





## 撤销索引、撤销表以及撤销数据库

------

通过使用 DROP 语句，可以轻松地删除索引、表和数据库。

------

### DROP INDEX 语句

DROP INDEX 语句用于删除表中的索引。

### 用于 MS Access 的 DROP INDEX 语法：

> DROP INDEX index_name ON table_name

### 用于 MS SQL Server 的 DROP INDEX 语法：

> DROP INDEX table_name.index_name

### 用于 DB2/Oracle 的 DROP INDEX 语法：

> DROP INDEX index_name

### 用于 MySQL 的 DROP INDEX 语法：

> ALTER TABLE table_name DROP INDEX index_name





------

## DROP TABLE 语句

DROP TABLE 语句用于删除表。

> DROP TABLE table_name

------



## DROP DATABASE 语句

DROP DATABASE 语句用于删除数据库。

> DROP DATABASE database_name

------



## TRUNCATE TABLE 语句

如果我们仅仅需要删除表内的数据，但并不删除表本身，那么我们该如何做呢？

请使用 TRUNCATE TABLE 语句：

> TRUNCATE TABLE table_name



