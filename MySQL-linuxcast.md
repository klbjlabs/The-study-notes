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
## Lesson 7 MySQL用户管理基础

### MySQL用户
* MySQL 数据库默认只有一个root用户
* MySQL 将用户的信息保存在mysql数据库user表中

### 创建一个新的用户

	CREATE USER 用户名 IDENTIFIED BY '密码';
	// 新用户创建后是不能登陆的 因为未设置权限。

### 删除一个用户

	DROP USER 用户名;

### 重命名一个用户
	
	RENAME USER 用户名 TO 新用户名;

### 修改用户密码

	SET PASSWORD = PASSWORD('新密码'); // 修改当前用户密码

	SET PASSWORD FOR 用户 = PASSWORD('新密码');  // 修改指定用户密码

---

## Lesson 8 MySQL权限管理基础

### 权限系统控制包含两个阶段
1. 检查一个用户是否能够链接
2. 检查用户是否具有所执行动作的权限

>### MySQL权限层级
1. 全局层级
2. 数据库层级
3. 表层级
4. 列层级
5. 子程序层级

### MySQL授权命令
MySQL通过GRANT授予权限，REVOKE撤销权限

	// 授予一个用户权限:
	GRANT ALL PRIVILEES ON 层级 to 用户名@主机 IDENTIFIED BY 密码;
	---
	// 授予klbj用户全局级全部权限:
	GRANT ALL PRIVILEES ON *.* to 'klbj'@'%' IDENTIFIED BY '123456';
	---
	// 授予klbj用户针对test数据库的全部权限:
	GRANT ALL PRIVILEGES ON test.* to 'klbj'@'%' IDENTIFIED BY '123456';
	---
	// 撤销一个用户权限
	REVOKE ALL PRIVILEGES FROM 用户名;
	---
	// 撤销klbj用户全部权限
	REVOKE ALL PRIVILEGES FROM klbj;

### MySQL连接认证

	'klbj'@'%'
	  |     `------主机
	  `---------用户名

>### 主机是指允许从那些主机进行连接，可以使用如下形式:
1. 所有主机: "%" ----(只能从远程连接登陆)
2. 精确的主机名或IP地址: www.xxx.com 192.168.1.1
3. 使用 "*" 通配符: *.xxx.com
4. 指定一个网段: 192.168.1.0/255.255.255.0


>赋予ROOT远程登陆权限(默认只能localhost连接)
	GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '123456';

---
## Lesson 9 MySQL简单的备份恢复(mysqldump)

### 备份一个指定的数据库:

	mysqldump -u root -p 数据库名 > 备份文件.sql

### 从备份的SQL文件恢复一个指定数据库:
	
	mysql -u root -p 数据库名称 < 备份文件.sql

## Lesson 10 MySQL数据库字符编码设置

### 数据库编码
> 数据库使用一个特定编码保存数据,如Latin、Big5、GB2132、UTF8等,不同语言一般使用不同编码保存

> 编码主要影响以下两个方面:
1. 数据库保存相同内容所占用的空间大小。
2. 数据库与客户端通信

### MySQL 编码
> MySQL数据库的默认编码是:

	character set: latin1
	cillation: latin1_swedish_ci

> 可以通过以下命令查看MySQL支持的编码:

	SHOW CHARACTER SET;
	







