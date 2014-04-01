##CLASS_1
> Oracle Database 基本核心文件
* Data files
* Contril files
* Redo Log files   --->  (Archived Log files 归档文件）

##CLASS_2
> Memory Structure
* System Global Area (SGA) [一个数据库只有一个SGA]
  * Shared Pool
  * Database Buffer Cache
  * Redo Log Buffer
  * Large Pool [可选]
  * Java Pool [可选]
* Program Global Area (PGA) [一个进程就有一个PGA]

##CLASS_3
> ###Process Structure
* User process
* Server process
* Background processes

> IPC (Inter Process Communication): 包括共享内存、队列、信号量等几种形式.

###Backgtound Process
* Mandatory background process:
	DBWn	PMON	CKPT
	LGWR	SMON
* Optional background process:
	ARCn	LMDn	QMNn
	CJQ0	LMON	RECO
	Dnnn	LMS	Snnn
	LCKn	Pnnn

---

## Chapter_2 Getting Started with the Oracle Server

###DB Administration Tools
* Oracle Universal Installer (OUI)
* Database Configuration Assistant (DBCA) 
* Database Upgrade Assistant (DUA)
* Oracle Net Manager 
* Oracle Enterprise Manager
* SQL\*Plus
* Recovery Manager
* Oracle Secure Backup
* Data Pump
* SQL\*Loader


#### Starting the OUI

	$ ./runInstaller

#### Oracle DBCA
* Create a database
* Configure database options
* Delete a database
* Manage templates

### DB Administrator Users
* SYS & SYSTEM
 * User SYS
  * Owner of the database data dictionary
  * Default password: change_on_install
 * User SYSTEM
  * Owner of additional internal tables and views used by Oracle yools
  * Default password: manager

### SQL*Plus - IMPORTANT!!!!

	sqlplus /nolog
	connect / as sysdba
### Oracle Enterprise Manager
* Oracle Management Server
* Repository

---

## Chapter_03_Managing an Oracle Instance
### Start Up

	CONNECT / AS SYSDBA
	STARTUP
	SHUTDOWN abort
### PFILE & SPFILE
* `PFILE` - $ORACLE_HOME/dbs/initSID.ora -  Need Restart 
* `SPFILE` - spfileSID.ora - Binary file - 即时生效 - 可用RMAN备份

### Creating a PFILE [old]

	cp init.ora $ORACLE_HOME/dbs/initSID.ora

### Creating a SPFILE (IN SQL*PLUS)

	CREATE SPFILE = '$ORACLE_HOME/dbs/spfileSID.ora'
	FROM PFILE = '$ORACLE_HOME/dbs/initSID.ora';
	---
	CREATE SPFILE FROM PFILE;  //PFILE -> SPFILE
	CREATE PFILE FROM SPFILE;  //SPFILE -> PFILE

#### Show SPFILE
	
	strings spfile |more ;  //查看SPFILE 中的内容

> SPFILE is better than PFILE!

### STARTUP Command Behavior
1. spfileSID.ora
2. Default SPFILE
3. initSID.ora
4. Default PFILE

`STARTUP PFILE="xxx/xxx.ora"` - 手工指定PFILE，SPFILE 不支持手动 但可以插入到PFILE中`spfile=$ORACLE_HOME/xx/spfileSID.ora`

### Who can start the DB?

### Start Up a Databases
1. SHUTDOWN
2. NOMOUNT [Instance Start] `startup nomount`
3. MOUNT [Control file opened for this instance] `alter database mount;`
4. OPEN [All files opened as described by the control file for this instance] `alter database open;`

### Restricted Mode

	STARTUP RESTRICT
	alter system enable restricted session;
	---
	select sid,serial#,username from v$session;
	alter system kill session 'sid,serial';  Kill

### Read-Only Mode
	
	STARTUP MOUNT
	ALTER DATABASE OPEN READ ONLY;

### Shutting Down the Database
1. Close a Database
2. Unmount a Database
3. ShutDown an Instance

#### Shutdown mode
* `A` - `ABORT`
* `I` - `IMMEDIATE`
* `T` - `TRANSACTIONAL`
* `N` - `NORMAL`

### Trace File
* alterSID.log
 * Records the commands
 * Records results of major events
 * Used for day-to-day operational information
 * Used for diagnosing database errors
 * Location defined by `BACKGROUND_DUMP_DEST`
* Background trace Files
 * Location defined by `BACKGROUND_DUMP_DEST`
* User trace files
 * Location is defined by `USER_DUMP_DEST`
 * Size defined by `MAX_DUMP_FILE_SIZE`
 * Enable/Disable User Tracing
  * Using the `ALTER SESSION SET SQL_TRACE=TRUE`

> show parameter dump

---
## Chapter 04 - Creating a Database

