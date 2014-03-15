# MySQL数据库基础
## Lesson 1 MySQL数据库安装及基本配置

### Install

	# yum list | grep mysql
	# yum install -y mysql-server mysql mysql-devel
	# rpm -qi mysql-server
	# service mysqld start

### Init

	# mysqladmin -u root password 'xxzxadmin'
	# mysql -u root -p

### Auto boot

	# chkconfig mysqld on

### Config File

* `/etc/my.conf` - Mysql 配置文件
* `/var/lib/mysql/` - 数据库存储目录 可在`/etc/my.conf`中修改`datadir=`字段为可靠的存储位置---如盘柜、网络存储等
* `/var/log/mysqld.log` - 日志文件

### 端口（默认的端口号为 TCP 3306）
	
	# netstat -tupln
	---
	Active Internet connections (only servers)
	Proto Recv-Q Send-Q Local Address               Foreign Address             State       PID/Program name   
	tcp        0      0 0.0.0.0:3306                0.0.0.0:*                   LISTEN      1235/mysqld       
---

## Lesson 2 MySQL数据库基本操作

### remote access mysql-server

	# mysql -h 192.168.1.105 -u root -p
### 常用命令

* `mysql> SELECT VERSION();` - 查看当前MySQL版本
* `mysql> SHOW DATABASES;` - 查看所有的数据库 其中 "test" 为试验用数据库可随意更改
* `mysql> CREATE DATABASE abc` - 创建名为 "abc" 的数据库
* `mysql> DROP DATABASE abc` - 删除名为 "abc" 的数据库
* `mysql> USE abc` - 将当前的数据库切换为 "abc"

> 数据库的名称不能修改

---

## Lesson 3 SQL语言基础 - 1

### SQL (Structured Query Language) 结构化查询语言
> * SQL是一个ANSI标准计算机语言，设计用来访问、操作数据库系统。 
> * 几乎所有现今的关系型数据库软件（MySQL, MS Access, DB2, Informix, MS SQL Server, Oracle, Sybase...）都是用SQL进行查询、管理及常用操作.

### SQL 能做什么？
> * 面向数据库执行查询 
> * 可从数据库取回数据
> * 可在数据库中插入新的记录
> * 可更新数据库中的数据
> * 可从数据库删除记录
> * 可创建新数据库
> * 可在数据库中创建新表
> * 可在数据库中创建存储过程
> * 可在数据库中创建视图
> * 可以设置表、存储过程和殊途的权限

### SQL 语句分类
> * **Data Definition Language (DDL)**
>   * `CREATE` - 在数据库中创建对象
>   * `ALTER` - 修改数据库结构
>   * `DROP` - 删除对象
>   * `RENAME` - 重命名对象
> * **Data Manipulation Language (DML)**
>   * `SELECT` - 从数据库中获取数据
>   * `INSERT` - 向一个表中插入数据
>   * `UPDATE` - 更新一个表中已有的数据
>   * `DELETE` - 删除表中的数据
> * **Data Control Language (DCL)**
>   * `GRANT` - 赋予一个用户对数据库或数据表的指定权限
>   * `REVOKE` - 删除一个用户对数据库或数据表的指定权限
> * **Transation Control (TCL)**
>   * `COMMIT` - 保存数据操作
>   * `SAVEPOINT` - 为方便rollback标记一个事务点
>   * `ROLLBACK` - 从最后一次COMMIT中恢复到提交前状态

---
## Lesson 4 SQL语言基础 - 2

### 创建数据库
* `CREATE DATABASE linuxcast;` - 创建数据库
* `DROP DATABASE linuxcast;` - 删除数据库
* `RENAME DATABASE linuxcast TO lcdb;` - 重命名数据库（已失效）

### 创建表

	CREATE TABLE 表名称(
	列名1 数据类型,
	列名2 数据类型,
	列名3 数据类型,
	...
	);

	---
	CREATE TABLE lc_course(
	id int,
	course_name varchar(100),
	course_length int,
	teacher varchar(50),
	category varchar(100)
	);
### 查看表结构

	DESCRIBE lc_course;

### 删除表
	
	DROP TABLE lc_course;

### 修改表

* `ALTER TABLE lc_course RENAME course;` - 重命名表	
* `ALTER TABLE lc_course ADD link varchar(100);` - 向表中添加一列	
* `ALTER TABLE lc_course DROP COLUMN link;` - 删除表中一列
* `ALTER TABLE lc_course MODIFY teacher varchar(100);` - 修改一个列的数据类型	
* `ALTER TABLE lc_course CHANGE COLUMN teacher lecture varchar(100);` - 重命名一个列

---

## Lesson 5 SQL语言基础 - 3

### SQL - 向表中插入数据

* `INSERT INTO 表名称 VALUES (值1, 值2, ...);` - 向表格中插入一条记录
* `INSERT INTO (列1, 列2) VLAUES (值1, 值2);` - 插入特定列的值
* `例` - `INSERT INTO course(1, 'Install Linux', 'nash_su', 'Basic');`

### SQL - 查询数据

* `SELECT 列名1,列名2... FROM 表名称;`
* `SELECT * FROM 表名称;`
* `例` - `SELECT course_name,category FROM course;`

### SQL - 按条件查询数据

* `SELECT 列名称 FROM 表名 WHERE 列 运算符 值;`
* `例` - `SELECT * FROM course WHERE course_name='GNOME';`
* `例` - `SELECT * FROM course WHERE course_length>10;`

#### SQL WHERE 支持的运算符

|操作符 |      功能     |
|:-----:|:-------------:|
|   =   |等于           |
| \<\>  |不等于         |
|  \>   |大于           |
|  \<   |小于           |
|  \>=  |大于等于       |
|  \<=  |小于等于       |
|BETWEEN|在某范围内     |
| LIKE  |搜索某种模式   |
>

### SQL - 删除一条记录

* `DELETE FROM 表名称 WHERE 列 运算符 值;` - `删除指定记录`
* `DELETE * FROM 表名称;` - `删除表中所有信息`

### SQL - 更新一条记录

* `UPDATE 表名称 SET 列名称 = 新值 WHERE 列=值;` - `更新指定记录`
* `例` - `UPDATE course SET lecture='Lee' WHERE id=3;`

---
## Lesson 6 SQL语言基础 - 4

### SQL - Distinct

* `SELECT DISTINCT 列名称 FROM 表名称;` - `返回结果删除重复项`
* `例` - `SELECT DISTINCT lecture FROM course;`

### SQL - AND & OR
> WHERE 条件中使用逻辑组合
	SELECT * FROM 表名称 WHERE 条件1 AND 条件2;
	SELECT * FROM 表名称 WHERE 条件1 OR 条件2;

### SQL - 对结果进行排序
> 对查询结果指定的列进行排序

* `SELECT * FROM 表名称 ORDER BY 列名;` - `正序`
* `SELECT * FROM 表名称 ORDER BY 列名 DESC;` - `倒序`

---
