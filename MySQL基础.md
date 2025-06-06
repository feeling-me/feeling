 mysql概述，SQL，函数，约束，多表查询，事务 六大块

# 零.额外知识点

## 1.联合查询-union，union all

### 语法

​	`select 字段列表 from 表A ...`

​	`union [all]`

​	`select 字段列表 from 表B ...;`

- 其实就是把两个查询结果放在同一个界面展示，更加直观
- **union all 会把全部数据直接合并在一起，union 会对合并之后的数据去重**
- **联合查询的多张表的列数必须保持一致，字段类型也需要保持一致**





# 一.MySQL概述（未完善）

关系数据库
建立在关系模型基础上，由多张相互连接的二维表组成的数据库
1.使用表存储数据，用SQL语言操作



# 二.SQL

1. ###  SQL通用语法

2. ###  SQL分类

3. ###  DDL

4. ###  DML

5. ###  DQL

6. ###  DCL




## 1.SQL通用语法

1.可以单行或多行书写，分号结尾；

2.可以用空格/缩进增强可读性；

3.不区分大小写，关键字建议大写；

4.注释：· 单行用 -- 或者 #(MySQL特有)

​		·多行注释用 /*... */



## 2.SQL分类

| 分类 | 中间字母含义 |                说明                |
| :--: | :----------: | :--------------------------------: |
| DDL  |  Definition  |       数据定义语言,定义对象        |
| DML  | Manipulation |      数据操作语言,数据增删改       |
| DQL  |    Query     |     数据查询语言,查询表的记录      |
| DCL  |   Control    | 数据控制语言,创建用户,控制访问权限 |



## 3.DDL

### (1)DDL-数据库操作

#### 查询

​	查询所有数据库：`show databases;`

​	查询当前数据库：`select database();`

#### 创建

​	`create database 数据库名;`

#### 删除

​	`drop database 数据库名;`

#### 使用

​	`use 数据库名;`

------

### (2)DDL-表操作-查询

#### 查询当前数据库所有表

​	`show tables;`

#### 查询表结构

​	`desc 表名;`

#### 查询指定表的建表语句

​	`show create table 表名;`

------

### (3)DDL-表操作-创建

​	`create table 表名(`

​			`字段1  字段1类型 (注释)comment '字段注释',`

​			`字段2  字段2类型 (注释)comment '字段注释,`

​			`字段n  字段n类型 (注释)comment '字段注释'`

`) (注释)comment '表注释';`

#### 字段类型

|   分类   |     类型     |  大小  |        描述        |
| :------: | :----------: | :----: | :----------------: |
|          |   tinyint    | 1 byte |      小整数值      |
|          |   smallint   | 2 byte |      大整数值      |
|          |  mediumint   | 3 byte |      大整数值      |
| 数据类型 | int或integer | 4 byte |      大整数值      |
|          |    bigint    | 8 byte |     极大整数值     |
|          |    float     | 4 byte |   单精度浮点数值   |
|          |    double    | 8 byte |   双精度浮点数值   |
|          |   decimal    |        | 小数值(精确定点数) |

 <u>decimal</u> 自定义几位。

例子：  age tinyint unsigned ,其中unsigned指的是无符号的范围，≥0

​		score double(**4,1**)——前一位数字指的是整体长度，后一位数字指的是小数位数



字符串类型：

|    分类    |    类型    |   大小(byte)    |             描述             |
| :--------: | :--------: | :-------------: | :--------------------------: |
|            |    char    |      0-255      |          定长字符串          |
|            |  varchar   |     0-65535     |          变长字符串          |
|            |  tinyblob  |      0-255      | 不超过255个字符的二进制数据  |
|            |  tinytext  |      0-255      |         短文本字符串         |
| 字符串类型 |    blob    |     0-65535     |    二进制形式的长文本数据    |
|            |    text    |     0-65535     |          长文本数据          |
|            | mediumblob |  0-16 777 215   | 二进制形式的中等长度文本数据 |
|            | mediumtext |  0-16 777 215   |       中等长度文本数据       |
|            |  longblob  | 0-4 294 967 295 |   二进制形式的极大文本数据   |
|            |  longtext  | 0-4 294 967 295 |         极大文本数据         |

一般blob用的并不多。

char()和varchar()都要跟数字，指的是最长几个字符，超出就报错。

例如：char(10)就算只输入一个字符，也算10个字符，其他空间用空格填补；varchar()会灵活改变。



日期时间类型：	

|   分类   |   类型    | 大小 |   范围    |        格式         | 描述 |
| :------: | :-------: | :--: | :-------: | :-----------------: | :--: |
|          |   date    |  3   |           |     YYYY-MM-DD      | 常用 |
|          |   time    |  2   |           |      HH:MM:SS       | 常用 |
| 日期类型 |   year    |  1   | 1907-2155 |        YYYY         |      |
|          | datetime  |  8   |           | YYYY-MM-DD HH:MM:SS | 常用 |
|          | timestamp |  4   |           | YYYY-MM-DD HH:MM:SS |      |

------

### (4)DDL-表操作-修改

#### 添加字段

​	`alter table 表名 add 字段名 类型(长度)  (注释)comment '';`

#### 修改数据类型

​	`alter table 表名 modify 字段名 新数据类型(长度);`

#### 修改字段名和字段类型

​	`alter table 表名 change 旧字段名 新字段名 类型(长度)   (注释)comment ' ';`

​	**例子：将nickname字段修改为username，类型为varchar(30)**

​	**语句：alter table emp change nickname username varchar(30) comment '昵称';**

#### 删除字段

​	`alter table 表名 drop 字段名;`

#### 修改表名

​	`alter table 表名 rename to 新表名;`

------

### (5)DDL-表操作-删除

#### 删除表

​	`drop table [if exists] 表名；`

#### 删除指定表，并且重新创建该表(数据没了，留下结构)

​	`truncate table 表名;`

------





## 4.DML-数据增删改


添加数据insert，修改数据update，删除数据delete

------

### (1)DML-添加数据

#### 给指定字段添加数据

​	`insert into 表名(字段名1, 字段名2, ...) values(值1, 值2, ...);`

#### 给全部字段添加数据

​	`insert into 表名 values(值1, 值2, ...);`

#### 批量添加数据

​	`insert into 表名 (字段名1, 字段名2, ...) values(值1, 值2, ...), (值1, 值2, ...), (值1, 值2, ...);`

​	`insert into 表名 values(值1, 值2, ...), (值1, 值2, ...), (值1, 值2, ...);`添加到所有字段

#### 【ATTENTION!】

- 插入数据时，指定的字段顺序需要与值的顺序是一一对应的。
- 字符串和日期型数据应该包含在引号中。
- 插入的数据大小，应该在字段的规定范围内。

------

### (2)DML-修改数据

​	`update 表名 set 字段名1 = 值1, 字段名2 = 值2, ...[where 条件];` 

- where后面跟的是符合条件的才被修改，可写可不写，如果没有条件，则会修改整张表的所有数据。

------

### (3)DML-删除数据

​	`delete from 表名 [where 条件];`

- delete语句的条件跟update一样。
- delete语句不能删除某一字段的值，如果要这么做，使用update语句，将其值设置为NULL。




## 5.DQL-数据查询语言

查询数据库中表的记录select

DQL-语法-单表查询

​	`select`

​		`字段列表`	**执行顺序第 4 位**

​	`from`

​		`表名列表`	**执行顺序第 1 位**

​	`where`

​		`条件列表`	**执行顺序第 2 位**

​	`group by`

​		`分组字段列表`	**执行顺序第 3 位**

​	`having`

​		`分组后条件列表`

​	`order by`

​		`排序字段列表`	**执行顺序第 5 位**

​	`limit`

​		`分页参数`	**执行顺序第 6 位**

- 输入顺序 ≠ 执行顺序


- 执行顺序影响的可能有别名的使用

#### 基本查询 select，from

#### 条件查询 where

#### 聚合函数 count，max，min，avg，sum

#### 分组查询 group by

#### 排序查询 order by

#### 分页查询 limit

------

### (1)DQL-基本查询

#### 语法

#### 查询多个字段

​	`select 字段1, 字段2, 字段3, ... from 表名;`

​	`select*from 表名;`

#### 设置别名

​	`select 字段1 [as 别名1], 字段2 [as 别名2], ... from 表名;`

​	`select name, datediff(curdate(),entrydate) as '入职天数' from emp order by 入职天数 asc;`

​	别名可写可不写，as也是可写可不写。中括号不用写，只是拿来提示用的。

​	要使用别名，设置完成之后直接用，不需要加引号

#### **去除**重复记录

​	`select distinct 字段列表 from 表名;`



### (2)DQL-条件查询  where

#### 语法

​	`select 字段列表 from 表名 where 条件列表;`

where后面是条件列表，也就是说条件可以不止一个

#### 条件

| 比较运算符         | 功能                                       |
| ------------------ | ------------------------------------------ |
| >                  | 大于                                       |
| >=                 | 大于等于                                   |
| <                  | 小于                                       |
| <=                 | 小于等于                                   |
| =                  | 等于                                       |
| <> 或 !=           | 不等于                                     |
| between .. and ... | 在某个范围之内，含最小最大，多选多         |
| in(...)            | 在in之后的括号列表中的值，有就选           |
| like 占位符        | 模糊匹配 ( _匹配单个字符, %匹配任意个字符) |
| is NULL            | 是NULL                                     |

| 逻辑运算符 | 功能     |
| ---------- | -------- |
| and 或 &&  | 并且     |
| or 或 \|\| | 或者     |
| not 或 !   | 非，不是 |

部分例子：

​	1.查询姓名是3个字的员工：select * from emp where idcard like '___'; [引号里面是3个下划线]

​	2.查询身份证号最后一位是X的员工：select * from emp where idcard like '%X';

​	   %指的是前面多少个字符无所谓，只要后面这个存在就找到它 ；也可以用下划线代替，几个字符就几个下划线。



### (3)DQL-聚合函数-配合分组查询使用

#### 语法

​	`select 聚合函数(字段列表) from 表名 [where 条件];`

将**一列数据**作为一个整体，进行纵向计算，常见的有：

| 函数  | 功能     |
| ----- | -------- |
| count | 统计数量 |
| max   | 最大值   |
| min   | 最小值   |
| avg   | 平均值   |
| sum   | 求和     |



### (4)DQL-分组查询

#### 语法

​	`select 字段列表 from 表名 [where 条件]  group by  分组字段名 [having  分组后过滤条件];`

#### where 和 having的区别

- 执行时机不同：where是分组之前进行过滤，不满足where条件就不参与分组；而having是分组之后对结果进行过滤。


- 判断条件不同：where不能对聚合函数进行判断，而having可以。

#### 注意

- 执行顺序： where > 聚合函数 > having;
- 分组之后，查询字段一般为聚合函数和分组字段，查询其他字段无任何意义。

#### 例子

- 根据性别分组，统计男性员工 和 女性员工的数量：

  `select gender, count(*) as '男员工和女员工的数量' from emp group by gender;`


- 根据性别分组，统计男性员工 和 女性员工的平均年龄：

  `select gender, avg(age) as '男性员工和女性员工的平均年龄' from emp group by gender;`

- 查询年龄小于58的员工，并且根据工作地址分组，获取员工数量大于等于3的工作地址

  `select workaddress,count(*) from emp where age <= 58 group by workaddress having count(*) >= 3;`




### (5)DQL-排序查询

#### 语法

​	`select 字段列表 from 表名 order by 字段1 排序方式,  字段2 排序方式2;`

#### 排序方式

​	ASC(ascending)：升序（默认）

​	DESC(descending)：降序

​	如果是多字段排序，当第一个字段值相同时，才会根据第二个字段进行排序。



### (6)DQL-分页查询

#### 语法

​	`select 字段列表 from 表名 limit 起始索引, 查询记录数;`

#### 注意

- 起始索引从 **0** 开始，**起始索引=（查询页码 - 1）* 每页显示记录数**；
- 分页查询是数据库的方言，不同的数据库有不同的实现，在MySQL中是limit；
- 如果查询的是第一页数据，起始索引可以省略，直接简写为 limit 10




## 6.DCL-数据控制语言

用来管理数据库用户，控制数据库的访问权限

### (1)DCL-管理用户

#### 查询用户

​	`use mysql;`

​	`select * from user;`

#### 创建用户

​	`create user '用户名'@'主机名' identified by '密码';`	本地主机才可以访问

​	`create user '用户名'@'%' identified by '密码';`		任意主机都可以访问

#### 修改用户密码

​	`alter user '用户名'@'主机名' identified with mysql_native_password by '新密码';`

#### 删除用户

​	`drop user '用户名'@'主机名';`

#### 注意

- @之间不能有空格
- 主机名可以用 % 通配，代表任意主机都可访问
- 该SQL语句一般操作较少



### (2)DCL-权限控制

#### 常用权限

|         权限         |        说明        |
| :------------------: | :----------------: |
| all , all privileges |      所有权限      |
|        select        |      查询数据      |
|        insert        |      插入数据      |
|        update        |      修改数据      |
|        delete        |      删除数据      |
|        alter         |       修改表       |
|         drop         | 删除数据库/表/视图 |
|        create        |   创建数据库/表    |



#### 查询权限

​	`show grants for '用户名'@'主机名';`

#### 授予权限

​	`grant 权限列表 on 数据库名.表名 to '用户名'@'主机名';`

​	如果给所有的数据库，所有的表授权，就可以写  * . *

#### 撤销权限

​	`revoke 权限列表 on 数据库名.表名 from '用户名'@'主机名';`

#### 注意

- 多个权限之间，使用逗号分隔。
- 授权时，数据库名和表名可以使用 * 进行通配，代表所有



# 三.函数

函数是指一段可以直接被另一段程序调用的程序或代码。

1. ### 字符串函数

2. ### 数值函数

3. ### 日期函数

4. ### 流程函数



## 1.字符串函数

常用字符串函数如下：`select 函数(参数);`

| 函数                       | 功能                                                    |
| -------------------------- | ------------------------------------------------------- |
| concat(S1, S2,..., Sn)     | 字符串拼接，将S1,S2,Sn拼接为一个字符串                  |
| Lower(str)                 | 将字符串str全部转为小写，只能写一个字符串               |
| upper(str)                 | 将字符串str全部转为大写，只能写一个字符串               |
| Lpad(str, n, pad)          | 左填充，用字符串pad对str左边进行填充，达到n个字符串长度 |
| rpad(str, n, pad)          | 右填充，用字符串pad对str右边进行填充，达到n个字符串长度 |
| trim(str)                  | 去掉字符串头部和尾部的空格                              |
| substring(str, start, len) | 返回从字符串str从start位置起的len个长度的字符串         |

### 例子1

​	用字符串-进行左填充，select lpad('hello',10,'-');

### 例子2

​	员工的工号统一更改为5位数，不足5位数的全部在前面补0

`update emp set worknum = lpad(worknum,5,'0');`



### 疑惑

​	左右填充返回的是字符串，如果是int等类型，需要先将lpad转换后的结果改为数值型才可以，可以用cast函数（虽然转换后还是不行，填充'1'就莫名可以了）

`update score set id = lpad(id,5,'1');`





## 2.数值函数

常见的数值函数如下：

| 函数       | 功能                               |
| ---------- | ---------------------------------- |
| ceil(x)    | 向上取整，小变大                   |
| floor(x)   | 向下取整，大变小                   |
| mod(x,y)   | 返回x/y的模，就是取整              |
| rand()     | 返回0~1内的随机数                  |
| round(x,y) | 求参数x的四舍五入的值，保留y位小数 |

### 例子

生成一个六位数的随机验证码

`select rpad(round(rand()*1000000,0),6,'0');`



## 3.日期函数

常见的日期函数如下：

| 函数                              | 功能                                              |
| --------------------------------- | ------------------------------------------------- |
| curdate()                         | 返回当前日期                                      |
| curtime()                         | 返回当前时间                                      |
| now()                             | 返回当前日期和时间                                |
| year(date)                        | 获取指定date的年份                                |
| month(date)                       | 获取指定date的月份                                |
| day(date)                         | 获取指定date的日期                                |
| date_add(date,INTERVAL expr type) | 返回一个日期/时间值加上一个时间间隔expr后的时间值 |
| datediff(date1, date2)            | 返回起始时间date1 和 结束时间date2 之间的天数     |

### 例子及注释

- 将当前时间往后推70个月：`select date_add(now(), INTERVAL 70 month);` 单位取决于最后的日期类型，INTERVAL也可以不大写，但是大写看起来直观一点


- datediff(date1, date2)：第一个时间 减去 第二个时间



## 4.流程函数

常用，实现条件筛选，从而提高语句的效率

| 函数                                                       | 功能                                                      |
| ---------------------------------------------------------- | --------------------------------------------------------- |
| IF(value, t, f)                                            | 如果value为true，则返回t，否则返回f                       |
| IFNULL(value1, value2)                                     | 如果value不为空，返回value1，否则返回value2               |
| CASE WHEN [val1] THEN [res1] ... ELSE [default] END        | 如果val1为true，返回res1，... 否则返回default默认值       |
| CASE [expr] WHEN [val1] THEN [res1] ... ELSE [default] END | 如果expr的值等于val1，返回res1，... 否则返回default默认值 |

case函数可以不止一个val，例如：case workaddress when '上海' then '一线城市' when '北京' then '一线城市' else '二线城市' end

### 例子

​	查询emp表员工的姓名和工作地址（如果是北京/上海等城市，输出一线城市，其他输出二线城市）

​	1.`select`

​	`name,`
	`(case workaddress when '上海' then '一线城市' when '北京' then '一线城市' else '二线城市' end) as '工作地址'`
	`from emp;`



​	2.`case when math >= 85 then '优秀' when math >=60 && math <85 then '及格' else '不及格' end) as '数学'`



# 四.约束

## 1.概述

### 概念

​	作用于表中字段的规则，用于限制存储在表中的数据

### 目的

​	保证数据库中数据的正确性、有效性和完整性

### 分类

|   约束   | 描述                                                     | 关键字      |
| :------: | -------------------------------------------------------- | ----------- |
| 非空约束 | 限制该字段的数据不能为NULL                               | NOT NULL    |
| 唯一约束 | 保证该字段的所有数据都是唯一，不重复的                   | UNIQUE      |
| 主键约束 | 主键是一行数据的唯一标识，要求非空且唯一                 | PRIMARY KEY |
| 默认约束 | 保存数据时，如果未指定该字段的值，则采用默认值           | DEFAULT     |
| 检查约束 | 保证字段值满足某一个条件                                 | CHECK       |
| 外键约束 | 用来让两张表的数据之间建立联系，保证数据的一致性和完整性 | FOREIGN KEY |

**自动增长：AUTO_INCREMENT**

**作用于表中字段上的，可以在创建/修改表时添加约束。**



## 2.约束演示

### 主键约束，自动增长

​	`id int primary key auto_increment comment '主键，自动增长';`

​	不能为空

### 非空约束

​	`name varchar(10) NOT NULL COMMENT '不为空';`

### 唯一约束

​	`name varchar(10) UNIQUE COMMENT '唯一';`

​	可以为空

### 检查约束

​	`age int unsigned check ( age<=120 ) comment '不取负号，检查年龄是否<=120'；`

### 默认约束

​	`status char(1) default '1' comment '设置默认值，类型要和字段名一致';`



## 3.外键约束

### 概念

​	外键用来让**两张表**的数据之间建立联系，从而保证数据的一致性和完整性。

![外键约束的主表和从表](C:\Users\Asus\OneDrive\Desktop\g\1742611612267.png)



- 子表也叫从表，父表也叫主表；
- 在数据库层面，这两张表并未建立外键关联，所以无法保证数据的一致性和完整性。


### 语法

#### 添加外键

方式一：建表时设置外键

​	`create table 表名(`

​			`字段名  数据类型,`

​			`......`

​			`CONSTRAINT [外键名称]  FOREIGN KEY (外键字段名) REFERENCES 主表 （主表列名)`

​	`);`

方式二：表创建好之后额外增加，外键名称可不用加引号

​	`alter table 表名 add constraint 外键名称 foreign key (外键字段名) references 主表(主表列名);`

#### 删除外键

​	`alter table 表名 drop foreign key 外键名称;`

#### 删除/更新行为以及其语法

| 行为        | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| NO ACTION   | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新。（和restrict用法一样）MySQL默认该行为 |
| RESTRICT    | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新。（和no action用法一样）MySQL默认该行为 |
| CASCADE     | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有，则也删除/更新外键在子表中的记录。 |
| SET NULL    | 当在父表中删除对应记录时，首先检查该记录是否有对应外键，如果有则设置子表中该外键值为null（这就要求外键允许取null） |
| SET DEFAULT | 父表右变更时，子表将外键设置成一个默认的值（innodb不支持，不用很了解） |

语法：

​	`alter table 表名 add constraint 外键名称 foreign key (外键字段) references 主表名(主字段名) on update cascade on delete cascade;`

on update cascade意思是在更新时有何行为，on delete cascade意思是在删除时有何行为



# 五.多表查询

其实也是DDL语句，之前学的是单表查询。

多表关系，多表查询概述，连接查询（内连接，外连接，自连接），子查询6大类，以及多表查询案例

## 1.多表关系

### 概述

各个表结构之间存在的各种联系，基本分为3种

- 一对多（多对一）
- 多对多
- 一对一



### (1) 一对多（多对一）

关系：一个部门对应多个员工，一个员工对应一个部门

实现：**在多的一方建立外键，指向“一”的一方建立主键**

### (2)多对多

关系：一个学生可以选多门课，一门课也可以被多个学生选择

实现：**建立第三张中间表，中间表至少包含两个外键，分别关联两方主键**

### (3)一对一

关系：多用于**单表拆分**，将一张表的基础字段放在一张表中，其他详情字段放在另一张表中

实现：**在任意一方加入外键，关联在另外一方的主键，并且设置外键为唯一的（unique）**



## 2.多表查询概述

- 查询多个表：`select * from 表名1,表名2,...;`,此时会出现笛卡尔积

- 笛卡尔积：指的是在数学中，两个集合  A集合和B集合的所有组合情况；在多表查询中，需要删除无效的笛卡尔积。

- 可以用where条件查询来限制

  ​

  连接查询——内连接，外连接，自连接

- 内连接：相当于查询A,B交集部分数据

- 外连接：

  - 左外连接：查询左表所有数据，以及两张表交集部分数据
  - 右外连接：查询右表所有数据，以及两张表交集部分数据

- 自连接：当前表与自身的连接查询，**自连接必须使用表别名**

  还有子查询



## 3.连接查询——内连接

内连接查询的是两张表交集部分

![图标示意](C:\Users\Asus\OneDrive\Desktop\g\1742702756697.png)

### 内连接查询语法

#### 隐式内连接

​	`select 字段列表 from 表1,表2 where 条件......;`

#### 显式内连接

​	`select 字段列表 from 表1 [inner] join 表2 on 连接条件...;`

​	inner可省略



## 4.连接查询——外连接

### 外连接查询语法

![图标示意](C:\Users\Asus\OneDrive\Desktop\g\1742702756697.png)

#### 左外连接

​	`select 字段列表 from 表1 LEFT [OUTER] JOIN 表2 ON 条件 ...;`

​	一般用左外，因为右外也可以改成左外。

​	相当于查询表1的所有数据，以及表1和表2交集部分的数据【蓝色和绿色部分】

#### 右外连接

​	`select 字段列表 from 表1 RIGHT [OUTER] JOIN 表2 ON 条件 ...`

​	相当于查询表2的所有数据，以及表1和表2交集部分的数据【黄色和绿色部分】

#### ！左右外连接巧记！

​	left join 左边，也就是查询写在**left join左边**的表的所有数据，以及两表交集

​	right join 右边，也就是查询写在**right join右边**的表的所有数据，以及两表交集



## 5.连接查询——自连接

### 语法

​	`select 字段列表 from 表A 别名A join 表A 别名B on 条件......`;

自连接查询，可以是内连接查询，也可以是外连接查询；

**必须起别名！！！**



## 6.子查询

### 概念

SQL语句中嵌套SELECT语句，称为嵌套查询，也叫子查询

**根据子查询的结果不同，可以分类为4类：**

1. 标量子查询（子查询结果为单个值）
2. 列子查询（子查询结果为一列）
3. 行子查询（子查询结果为一行）
4. 表子查询（子查询结果为多行多列）

**根据子查询位置，可以分为：**

WHERE之后, FROM之后, SELECT之后。

### 语法

​	`select * from t1 where column1 = (select column from t2);`

子查询外部的语句可以是insert/update/delete/select的任意一个

### 标量子查询

​	子查询返回的结果是单个值（数字，字符串，日期等），最简单的形式

​	**常用的操作符有：=，<>，>，>=，<，<=**

 	例子：查询在“小四”入职之后的员工信息

​	`select * from emp where entrydate > (select entrydate from emp where id = 4);`

### 列子查询

​	子查询返回的结果是一列（可以多行），被称为列子查询

​	**常用的操作符有：IN，NOT IN，ANY，SOME，ALL**

| 操作符 | 描述                                 |
| :----: | ------------------------------------ |
|   IN   | 在指定的集合范围之内，有符合的就选   |
| NOT IN | 不在指定的集合范围之内               |
|  ANY   | 子查询返回列表中，有任意一个满足即可 |
|  SOME  | 与ANY等同，使用SOME的地方都可以用ANY |
|  ALL   | 子查询返回列表的所有值都必须满足     |

​	例子：查询比研发部所有人工资都高的员工信息

​	`select * from emp where salary > all (select emp.salary from emp where dept_id = (select id from dept where name = '研发部'));`

### 行子查询

​	子查询返回回来的结果是一行（可以是多列），称为行子查询。

​	**常用的操作符：=、<>、IN、NOT IN**

​	例子：查询和“小一”相同薪资和相同直属领导的员工，可以把两个条件用逗号连接起来

​	`select * from emp where (salary,managerid) = (select salary, managerid from emp where name = '小一');`

​	`select * from emp where (salary,managerid) = (12500,1);`

### 表子查询

​	返回的结果是多行多列，称为表子查询。

​	**常用操作符：IN**

​	例子：

1.查询与小四，小五的职位和薪资相同的员工信息

​	`select * from emp where (job, salary) in (select job, salary from emp where name = '小四' or name = '小五');`

2.查询入职日期是“2003-01-01”之后的员工信息,及其部门信息

​	`select e.* , dept.* from (select * from emp where entrydate > '2003-01-01') as e left join dept on e.dept_id = dept.id;`

PS：将（select * from emp where entrydate > '2003-01-01'）**查询到的结果作为一张临时表**并且起好别名，再左外连接dept表，查询 临时表的员工id等于部门表的部门id 的结果





# 六.事务

​	事务简介，事务操作，事务四大特性，并发事务问题，事务隔离级别 5 大类

## 1.事务简介

​	一组操作的集合，把所有的操作作为一个整体一起向系统提交或撤销操作请求，这些操作**要么同时成功，要么同时失败**。一条SQL语句就是一个事务。



## 2.事务操作

### 查看/设置事务提交方式

​	`select @@autocommit;`

​	`set @@autocommit = 0;`

​	第一条语句是查询当前事务的提交方式是什么，如果为1则是自动提交，为0则是手动提交。

### 开启事务

​	在不修改事务的提交方式的情况下，控制事务

​	`start transaction;` 或 `begin;`

### 提交事务

​	`commit;`

​	手动提交状态下，执行这条语句才会更新表格数据

### 回滚事务(回到初始状态)

​	`rollback;`



## 3.事务四大特性

### 原子性

​	事务是不可分割的最小操作单元，要么全部成功，要么全部失败

### 一致性

​	事务完成时，必须使所有数据保持一致状态

### 隔离性

​	数据库系统提供的隔离机制，保证事务在不受外部并发操作影响的独立环境下运行

### 持久性

​	事务一旦提交或回滚，改变则是永久的



## 4.并发事务问题

|    问题    |                             描述                             |
| :--------: | :----------------------------------------------------------: |
|    脏读    |           一个事务读到另外一个事务还没有提交的数据           |
| 不可重复读 |       一个事务先后读取同一条记录，但两次读取的数据不同       |
|    幻读    | 一个事务按照条件查询数据时，没有对应的数据行，但是在插入数据时，又发现这行数据已经存在 |



## 5.事务隔离级别

|            隔离级别            | 脏读 | 不可重复读 | 幻读 |
| :----------------------------: | :--: | :--------: | :--: |
|   Read uncommitted 读未提交    |  √   |     √      |  √   |
|    Read committed 读已提交     |  ×   |     √      |  √   |
| Repeatable Read 可重复读(默认) |  ×   |     ×      |  √   |
|      Serializable 串行化       |  ×   |     ×      |  ×   |

​	PS：“√” 指的是会发生， “×” 指的是不会发生

​	**从上到下，性能由最优到最差，安全性由最差到最优**

### 查看事务隔离级别

​	`select @@transaction_isolation;`

### 设置事务隔离级别

​	`set [session 或 global] transaction isolation level [Read uncommitted 或 Read committed 或 Repeatable Read 或 Serializable]`

​	**session仅代表针对当前客户端窗口有效；global针对所有客户端的会话窗口有效**















