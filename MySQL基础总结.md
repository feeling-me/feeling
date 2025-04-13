# 一.DDL-数据定义语言

## 1.DDL-数据库操作

1. ​	查询所有数据库：`show databases;`

	.  	查询当前处于哪个数据库：`select database();`

	. ​	创建数据库：`create database [if not exists] 数据库名;`

	. ​	使用哪个数据库：`use 数据库名;`

	. ​	删除数据库：`drop database [if exists] 数据库名;`



## 2.DDL-表操作(该字段名和字段类型的，跟数据无关)

1. ​	查询当前数据库所有表：`show tables;`

	. ​	创建新表：`create table 表名(字段 字段类型, ...);`

	. ​	查询表结构：`desc 表名;`

	.  	查询指定表的建表语句：`show create table 表名;`

	.  	添加字段/修改数据类型/修改字段名和字段类型/删除字段/修改表名：`alter table 表名 add/modify/change/drop/rename to...;`

	.  	删除表格：`drop table [if exists] 表名；`

	.  	删除表格数据，留下结构：`truncate table 表名;`


 ​

# 二.DML-数据增删改

1. ​	添加数据：`insert into 表名(字段1,字段2,...) values(值1,值2,...)   [,(值1,值2,...)...];`
  .  	修改数据：`update 表名 set 字段名1 = 值1, 字段名2 = 值2, ...[where 条件];`
  . 	删除数据：`delete from 表名  [where 条件];`




# 三.DQL-数据查询语言

DQL语句

​	`select`	字段列表 —— 字段名 [as] 别名

​	`from`	表名

​	`where`	条件列表 —— 分组之前过滤 ; >, >=, <, <=, <>/!=, like '_/%', between ... and ..., in(), and, or

​	`group by` 分组字段列表

​	`having`	分组后条件列表 —— 分组之后过滤

​	`order by`	排序字段列表 —— 升序asc，降序desc

​	`limit`	分页参数 —— 起始索引=(要查看的页数 - 1)*每页展示记录数



# 四.DCL-数据控制语言

## 1.用户管理

​	创建用户：`create user '用户名'@'主机名' identified by 密码;`

​	修改用户密码：`alter user '用户名'@'主机名' identified with mysql_native_password by '新密码';`

​	删除用户：`drop user '用户名'@'主机名';`



## 2.权限控制

​	授予权限：`grant 权限列表 on 数据库名.表名 to '用户名'@'主机名';`

​	撤销权限：`revoke 权限列表 on 数据库名.表名 from '用户名'@'主机名';`



# 五.函数

## 1.字符串函数

​	字符串拼接：`CONCAT(S1,S2,...,Sn)`

​	字符串全部大/小写转换：`UPPER/LOWER(str)`

​	字符串左/右填充：`LPAD/RPAD(str,n,pad)`

​	去除左右两侧空格：`TRIM(str)`

​	截取字符串：`SUBSTRING(str,start,len)`



## 2.数值函数

​	向上/向下取整(向上小变大)：`CEIL/FLOOR(x)`

​	求模(x除以y的整数部分)：`MOD(x,y)`

​	求0~1之间的随机数：`RAND()`

​	四舍五入x，保留指定y位小数：`ROUND(x,y)`



## 3.日期函数

​	获取当前日期：`CURDATE()`

​	获取当前时间：`CURTIME()`

​	获取当前日期和时间：`NOW()`

​	获取指定的年份/月份/日期：`YEAR/MONTH/DAY(date)`

​	添加指定的时间周期：`DATE_ADD(date,INTERVAL,expr type)`

​	计算两个时间点之间的差(d1-d2)：`DATEDIFF(date1,date2)`



## 4.流程函数

​	判断第一个条件表达式是否为TRUE，为TRUE返回第2个参数，否则返回第3个参数：`IF(value, t, f)`

​	判断第一个参数是否为NULL，如果是NULL则返回第2个参数，不是则返回当前第1个参数：`IFNULL(value1,value2)`

​	条件分支的判断：`CASE [expr] WHEN [val1] THEN [res1] ... ELSE [default] END`

​	以及   `CASE WHEN [val1] THEN [res1] ... ELSE [default] END`



# 六.约束

## 1.非空约束

​	`NOT NULL`

## 2.唯一约束

​	`UNIQUE`

## 3.主键约束

​	`PRIMARY KEY (自增：AUTO_INCREMENT)`

## 4.默认约束

​	`DEFAULT`

## 5.检查约束

​	`CHECK`

## 6.外键约束

​	`FOREIGN KEY`

### 1)添加外键方式一：建表时设置外键

​	在括号中写：`CONSTRAINT [外键名称]  FOREIGN KEY (外键字段名) REFERENCES 主表 （主表列名)`

### 2)添加外键方式二：输入语句

​	语法：`alter table 表名 add constraint 外键名称 foreign key (外键字段名) references 主表(主表列名);`

### 3)删除外键

​	`alter table 表名 drop foreign key 外键名称;`

### 4)删除/更新行为以及其语法

​	当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新，默认行为：

​	**`NO ACTION 和 RESTRICT`**

​	当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有，则也删除/更新外键在子表中的记录：

​	**`CASCADE`**

​	当在父表中删除对应记录时，首先检查该记录是否有对应外键，如果有则设置子表中该外键值为null（这就要求外键允许取null）：

​	**`SET NULL`**

​	父表右变更时，子表将外键设置成一个默认的值（innodb不支持，不用很了解）：

​	**`SET DEFAULT`**

语法：

​	`alter table 表名 add constraint 外键名称 foreign key (外键字段) references 主表名(主字段名) on update cascade on delete cascade;`

on update cascade意思是在更新时有何行为，on delete cascade意思是在删除时有何行为



# 七.多表查询

## 1.多表关系

​	一对多：在多的一方设置外键，关联一的一方的主键

​	多对多：建立中间表，中间表包含两个外键，关联两张表的主键

​	一对一：用于表结构拆分，在其中任何一方设置外键（UNIQUE），关联另一方主键

## 2.多表查询

### 内连接

​	表AB的交集部分

#### 	隐式内连接

​	`select ... from 表A, 表B where 条件...`

#### 	显式内连接

​	`select ... from 表A [inner] join 表B on 条件 ...`

### 外连接

​	完全包含表A或表B的数据

#### 	左外

​	`select ... from 表A left join 表B on 连接条件 ...`

#### 	右外

​	`select ... from 表A right join 表B on 连接条件 ...`

### 自连接

​	`select ... from 表A 别名1, 表A 别名2 where 条件...`

### 子查询

​	标量子查询，列子查询，行子查询，表子查询



# 八.事务

## 1.事务简介

事务是一组操作的集合，这组操作要么全部执行成功，要么全部执行失败



## 2.事务操作

### 开启事务

​	`START TRANSACTION;`

### 提交/回滚事务

​	`COMMIT/ROLLBACK;`



## 3.事务四大特性

​	原子性、一致性、隔离性、持久性



## 4.并发事务问题

​	脏读，不可重复读，幻读



## 5.事务隔离级别

​	`READ UNCOMMITTED` ,  `READ COMMITTED` ,  `REPEATABLE READ` ,  `SERIALIZABLE`







​	

