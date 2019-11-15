数据库的基本使用  
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
show tables;

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
