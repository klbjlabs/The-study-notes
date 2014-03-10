##Chapter 1

###Install

	# yum list | grep mysql
	# yum install -y mysql-server mysql mysql-devel
 	# rpm -qi mysql-server
	# service mysqld start

##Init

	# mysqladmin -u root password 'xxzxadmin'
	# mysql -u root -p

###Auto boot

	# chkconfig mysqld on

###Config File
* `/etc/mysql.conf`	// Mysql config file
* `/var/lib/mysql/`	// Database dir /cun chu zai ke kao de cun chu wei zhi
			// ru pan gui, wang luo cun chu
* `/var/log/mysqld.log`	// ri zhi wen jian

###Port
	
	# netstat -tupln //  Default Port 3306 TCP
	---
	Active Internet connections (only servers)
	Proto Recv-Q Send-Q Local Address               Foreign Address             State       PID/Program name   
	tcp        0      0 0.0.0.0:3306                0.0.0.0:*                   LISTEN      1235/mysqld       
---

##Chapter 2

###remote access mysql-server

	# mysql -h 192.168.1.105 -u root -p



