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

* `/etc/my.conf`	 Mysql 配置文件
* `/var/lib/mysql/`	 数据库存储目录 可在`/etc/my.conf`中修改`datadir=`字段为可靠的存储位置---如盘柜、网络存储等
* `/var/log/mysqld.log`	 日志文件

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

* `mysql> SELECT VERSION();`	查看当前MySQL版本
* `mysql> SHOW DATABASES;`	查看所有的数据库 其中 "test" 为试验用数据库可随意更改
* `mysql> CREATE DATABASE abc`	创建名为 "abc" 的数据库
* `mysql> DROP DATABASE abc`	删除名为 "abc" 的数据库
* `mysql> USE abc`		将当前的数据库切换为 "abc"

> 数据库的名称不能修改

---

## Lesson 3 SQL语言基础 - 1

### SQL (Structured Query Language) 结构化查询语言
> * SQL是一个ANSI标准计算机语言，设计用来访问、操作数据库系统。 
> * 几乎所有现今的关系型数据库软件（MySQL, MS Access, DB2, Informix, MS SQL Server, Oracle, Sybase...）都是用SQL进行查询、管理及常用操作.
