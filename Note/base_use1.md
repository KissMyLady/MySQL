数据库的基本使用  
====
## 数据库介绍  
- [MySQL官方网站](https://www.mysql.com/)  

## 特点  
- 使用C和C++编写，并使用了多种编译器进行测试，保证源代码的可移植性  
- 支持多种操作系统，如Linux、Windows、AIX、FreeBSD、HP-UX、MacOS、NovellNetware、OpenBSD、OS/2 Wrap、Solaris等  
- 为多种编程语言提供了API，如C、C++、Python、Java、Perl、PHP、Eiffel、Ruby等  
- 支持多线程，充分利用CPU资源  
- 优化的SQL查询算法，有效地提高查询速度  
- 提供多语言支持，常见的编码如GB2312、BIG5、UTF8  
- 提供TCP/IP、ODBC和JDBC等多种数据库连接途径  
- 提供用于管理、检查、优化数据库操作的管理工具  
- 大型的数据库。可以处理拥有上千万条记录的大型数据库  
- 支持多种存储引擎  
- MySQL 软件采用了双授权政策，它分为社区版和商业版，由于其体积小、速度快、总体拥有成本低，  
  尤其是开放源码这一特点，一般中小型网站的开发都选择MySQL作为网站数据库  
- MySQL使用标准的SQL数据语言形式  
- Mysql是可以定制的，采用了GPL协议，你可以修改源码来开发自己的Mysql系统
- 在线DDL更改功能
- 复制全局事务标识
- 复制无崩溃从机
- 复制多线程从机

- MySQL是一个关系型数据库管理系统，由瑞典MySQL AB公司开发，后来被Sun公司收购，
Sun公司后来又被Oracle公司收购，目前属于Oracle旗下产品

> 开源 免费 不要钱 使用范围广,跨平台支持性好,提供了多种语言调用的 API  
> 是学习数据库开发的首选  

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

## 先来个小目标  
- 熟练编写，增删改查  
- 在Python中操作数据库  
![databases_summary]()

都坐下，基本操作    
====
## 命令行连接  
- 在工作中主要使用命令操作方式，要求熟练编写  
- 打开终端，运行命令  
```SQL
mysql -uroot -p
回车后输入密码，当前设置的密码为mysql
```

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
![databases_commed]()  
