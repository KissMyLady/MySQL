数据库的基本使用  
====
## 数据库安装  
1、安装Mysql服务器   
```Linux
sudo apt-get install mysql-server
```
2、启动服务器  
```Linux
sudo service mysql start

ps ajx|grep mysql
sudo service mysql stop
sudo service mysql restart
```
### 命令行客户端安装  
```Linux
sudo apt-get install mysql-client
```

都坐下，基本操作    
====
## 命令行连接  
- 在工作中主要使用命令操作方式，要求熟练编写  
- 打开终端，运行命令  
```SQL
mysql -uroot -p
回车后输入密码，当前设置的密码为mysql
```
最新的Ubuntu18.04安装最新的MySQL是没有密码设置选项的     
需要root账户, 进入mysql配置文件查看账户密码并修改    
[点击进入--如何重置密码](https://github.com/KissMyLady/MySQL/blob/master/Note/FORGET_PASSWORD.md)  

## 退出登录  
```SQL
quit 和 exit
或
ctrl+d
```  
- 登录成功后，输入如下命令查看效果  
```SQL   
查看版本：select version();
显示当前时间：select now();
```
##  修改输入提示符  
```SQL 
prompt python>
```
- \D 完整日期  
- \U 使用用户  

数据库
==== 

- 查看所有数据库  
```SQL 
show databases;
```
- 使用数据库
```SQL 
use 数据库名;
```
- 查看当前使用的数据库
```SQL 
select database();
```
- 创建数据库
```SQL 
create database 数据库名 charset=utf8;
例：
create database python charset=utf8;
```
- 删除数据库
```SQL 
drop database 数据库名;
例：
drop database python;
```


数据表  
==== 
- 查看当前数据库中所有表
```SQL
show tables;
```

- 查看表结构
desc 表名;
创建表
```SQL
auto_increment表示自动增长
CREATE TABLE table_name(
    column1 datatype contrai,
    column2 datatype,
    column3 datatype,
    .....
    columnN datatype,
    PRIMARY KEY(one or more columns)
);
```

- 例：创建班级表
```SQL
create table classes(
    id int unsigned auto_increment primary key not null,
    name varchar(10)
);
```

- 例：创建学生表
```SQL
create table students(
    id int unsigned primary key auto_increment not null,
    name varchar(20) default '',
    age tinyint unsigned default 0,
    height decimal(5,2),
    gender enum('男','女','人妖','保密'),
    cls_id int unsigned default 0
)
```

- 修改表-添加字段  
```SQL
alter table 表名 add 列名 类型;
例：
alter table students add birthday datetime;
```

- 修改表-修改字段：重命名版  
```SQL
alter table 表名 change 原名 新名 类型及约束;
例：
alter table students change birthday birth datetime not null;
``` 

- 修改表-修改字段：不重命名版
```SQL
alter table 表名 modify 列名 类型及约束;
例：
alter table students modify birth date not null;
```

- 修改表-删除字段
```SQL
alter table 表名 drop 列名;
例：
alter table students drop birthday;
```

- 删除表
```SQL
drop table 表名;
例：
drop table students;
```

- 查看表的创建语句
```SQL
show create table 表名;
例：
show create table classes;
```

## 特点  
> 开源 免费 好用 不要钱 使用范围广 

## RDBMS    
![12](https://github.com/KissMyLady/MySQL/blob/master/Img/mysql_structure.jpg)
> Relational Database Management System  
- 当前主要使用两种类型的数据库：关系型数据库、非关系型数据库，我们主要讨论关系型数据库，对于非关系型数据库,请看后面介绍
- 所谓的关系型数据库RDBMS，是建立在关系模型基础上的数据库，借助于集合代数等数学概念和方法来处理数据库中的数据
- 查看数据库排名:https://db-engines.com/en/ranking
* 关系型数据库的主要产品：  
    * oracle：在以前的大型项目中使用,银行,电信等项目  
     * mysql：web时代使用最广泛的关系型数据库  
    * ms sql server：在微软的项目中使用  
    * sqlite：轻量级数据库，主要应用在移动平台  

### SQL语句主要构成  
* DQL：数据查询语言，用于对数据进行查询，如select  
* DML：数据操作语言，对数据进行增加、修改、删除，如insert、udpate、delete  
* TPL：事务处理语言，对事务进行处理，包括begin transaction、commit、rollback  
* DCL：数据控制语言，进行授权与权限回收，如grant、revoke  
* DDL：数据定义语言，进行数据库、表的管理等，如create、drop  
* CCL：指针控制语言，通过控制指针完成表的操作，如declare cursor  

## 总 结  
![databases_commed](https://github.com/KissMyLady/MySQL/blob/master/Img/databases_commed.png)  
![databases_summary](https://github.com/KissMyLady/MySQL/blob/master/Img/databases_summary.png)


## 看完了  
- [数据库的基本使用](https://github.com/KissMyLady/MySQL/edit/master/Note/base_use1.md)
- [基础-增删改查](https://github.com/KissMyLady/MySQL/blob/master/Note/add_del_change_select.md)
- [数据库备份与恢复](https://github.com/KissMyLady/MySQL/blob/master/Note/backup_and_restore.md)
- [数据库规范与设计](https://github.com/KissMyLady/MySQL/blob/master/Note/design_databases.md)
- [返回主页](https://github.com/KissMyLady/MySQL)

友情链接 - [MySQL官方网站](https://www.mysql.com/)  
