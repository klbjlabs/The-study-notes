#Chapter 1

##Install
	yum install -y mysql-server mysql mysql-devel
	rpm -qi mysql-server
	service mysqld start
##Init
	mysqladmin -u root password 'xxzxadmin'
	mysql -u root -p
##Auto boot
	chkconfig mysqld on
