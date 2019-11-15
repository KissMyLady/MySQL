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






