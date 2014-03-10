Chapter 1

###Install
	# yum install -y mysql-server mysql mysql-devel
 	# rpm -qi mysql-server
	# service mysqld start
##Init
	# mysqladmin -u root password 'xxzxadmin'
	# mysql -u root -p
###Auto boot
	#  chkconfig mysqld on

###Config File
* `/etc/mysql.conf`	// Mysql config file
* `/var/lib/mysql/`	// Database dir /cun chu zai ke kao de cun chu wei zhi
			// ru pan gui, wang luo cun chu
* `/var/log/mysqld.log`	// ri zhi wen jian

###Create Database
	
	# netstat -tupln //  Default Port 3306 TCP



