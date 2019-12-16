MySQL主从同步配置  
====


## 常用命令  　　
配置文件地址：　　
```Linux
cd /etc/mysql/mysql.conf.d
sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
```
刷新权限：　　
```Linux
flush privileges;
stop slave;
```
修改日志文件:　 　　  
```Linux
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
```
监听日志:   　　
```Linux
sudo tail -f /var/log/mysql/mysql.log
sudo cat /var/log/mysql/mysql.log
```
监听错误日志:  　　
```Linux
sudo tail -f //var/log/mysql/error.log
vi /var/log/mysql/error.log
```
备 份：　　    
```Linux
mysqldump -uroot -pmysql --all-databases --lock-all-tables > ~/master_db.sql
```
恢 复：　　  
```Linux
mysql –uroot –pmysql < master_db.sql
```

## 在主服务器上创建账户命令 　       
```Linux  　
创建账户:                   所有数据库里的所有表
grant replication SLAVE ON *.* TO 'slave_ABC'@'%' identified by 'slave_ABC';
刷新命令   
FLUSH PRIVILEGES;　
```


## 主--MASTER   
显示主服务器信息   　　 
```Linux　　　
show master status;　　
+------------------+----------+--------------+------------------+-------------------+
| File             | Position | Binlog_Do_DB | Binlog_Ignore_DB | Executed_Gtid_Set |
+------------------+----------+--------------+------------------+-------------------+
| mysql-bin.000005 |      590 |              |                  |                   |
+------------------+----------+--------------+------------------+-------------------
1 row in set (0.00 sec)　　　
```

### 从服务器连接到主服务器:      
 ```Linux　　
change master to 　
	  master_host='10.211.55.5', 　　
	  master_user='slave', 
	  master_password='slave',
  	master_log_file='mysql-bin.000005', 
  	master_log_pos=590;

show slave status \G;  
show master status;
sudo service mysql restart
mysql -uroot -p
```


## 1. 主从同步的定义  
主从同步使得数据可以从一个数据库服务器复制到其他服务器上，在复制数据时，一个服务器充当主服务器（master），  
其余的服务器充当从服务器（slave）。因为复制是异步进行的，所以从服务器不需要一直连接着主服务器，  
从服务器甚至可以通过拨号断断续续地连接主服务器。通过配置文件，可以指定复制所有的数据库，某个数据库，甚至是某个数据库上的某个表。  
读写分离；数据备份。  

使用主从同步的好处：

- 通过增加从服务器来提高数据库的性能，在主服务器上执行写入和更新，在从服务器上向外提供读功能，可以动态地调整从服务器的数量， 
 从而调整整个数据库的性能。

- 提高数据安全，因为数据已复制到从服务器，从服务器可以终止复制进程，所以，可以在从服务器上备份而不破坏主服务器相应数据  

- 在主服务器上生成实时数据，而在从服务器上分析这些数据，从而提高主服务器的性能  


## 2. 主从同步的机制  
 ![]()  
Mysql服务器之间的主从同步是基于二进制日志机制，主服务器使用二进制日志来记录数据库的变动情况，  
从服务器通过读取和执行该日志文件来保持和主服务器的数据一致。

在使用二进制日志时，主服务器的所有操作都会被记录下来，然后从服务器会接收到该日志的一个副本。  
从服务器可以指定执行该日志中的哪一类事件（譬如只插入数据或者只更新数据），默认会执行日志中的所有语句。  

每一个从服务器会记录关于二进制日志的信息：文件名和已经处理过的语句，  
这样意味着不同的从服务器可以分别执行同一个二进制日志的不同部分，并且从服务器可以随时连接或者中断和服务器的连接。  

主服务器和每一个从服务器都必须配置一个唯一的ID号（在my.cnf文件的[mysqld]模块下有一个server-id配置项），  
另外，每一个从服务器还需要通过CHANGE MASTER TO语句来配置它要连接的主服务器的ip地址，  
日志文件名称和该日志里面的位置（这些信息存储在主服务器的数据库里）  


## 3. 配置主从同步的基本步骤  
有很多种配置主从同步的方法，可以总结为如下的步骤：  

1、在主服务器上，必须开启二进制日志机制和配置一个独立的ID  
2、在每一个从服务器上，配置一个唯一的ID，创建一个用来专门复制主服务器数据的账号  
3、在开始复制进程前，在主服务器上记录二进制文件的位置信息  
4、如果在开始复制之前，数据库中已经有数据，就必须先创建一个数据快照（可以使用mysqldump导出数据库，或者直接复制数据文件）  
5、配置从服务器要连接的主服务器的IP地址和登陆授权，二进制日志文件名和位置  

## 4. 详细配置主从同步的方法  
主和从的身份可以自己指定，我们将虚拟机Ubuntu中MySQL作为主服务器，  
将Windows中的MySQL作为从服务器。 在主从设置前，要保证Ubuntu与Windows间的网络连通。  

### 4.1 备份主服务器原有数据到从服务器  
如果在设置主从同步前，主服务器上已有大量数据，可以使用mysqldump进行数据备份并还原到从服务器以实现数据的复制。  

### 4.1.1 在主服务器Ubuntu上进行备份，执行命令：  
```SQL
mysqldump -uroot -pmysql --all-databases --lock-all-tables > ~/master_db.sql
```  
说 明    

* -u ：用户名  
* -p ：示密码  
* --all-databases ：导出所有数据库  
* --lock-all-tables ：执行操作时锁住所有表，防止操作时有数据修改  
* ~/master_db.sql :导出的备份数据（sql文件）位置，可自己指定  


### 4.1.2 在从服务器Windows上进行数据还原  
找到Windows上mysql命令的位置  
![]()  

新打开的命令窗口，在这个窗口中可以执行类似在Ubuntu终端中执行的mysql命令



将从主服务器Ubuntu中导出的文件复制到从服务器Windows中，可以将其放在上面mysql命令所在的文件夹中，方便还原使用
![]()  

在刚打开的命令黑窗口中执行还原操作:
```SQL
mysql –uroot –pmysql < master_db.sql
```


## 其他又情链接  
- [MYSQL官方文档](https://dev.mysql.com/doc/refman/8.0/en/change-master-to.html)






