账户管理  
====
- 在生产环境下操作数据库时，绝对不可以使用root账户连接，而是创建特定的账户，  
授予这个账户特定的操作权限，然后连接进行操作，主要的操作就是数据的crud

* MySQL账户体系：根据账户所具有的权限的不同，MySQL的账户可以分为以下几种
  * 服务实例级账号：，启动了一个mysqld，即为一个数据库实例；如果某用户如root,拥有服务实例级分配的权限，  
  那么该账号就可以删除所有的数据库、连同这些库中的表  
  
  * 数据库级别账号：对特定数据库执行增删改查的所有操作  
  * 数据表级别账号：对特定表执行增删改查等所有操作  
  * 字段级别的权限：对某些表的特定字段进行操作  
  * 存储程序级别的账号：对存储程序进行增删改查的操作  

-账户的操作主要包括创建账户、删除账户、修改密码、授权权限等  

注 意：

1、进行账户操作时，需要使用root账户登录，这个账户拥有最高的实例级权限  
2、通常都使用数据库级操作权限  


## 授予权限  
需要使用实例级账户登录后操作，以root为例  
 
主要操作包括：  

查看所有用户  
修改密码  
删除用户  

## 1. 查看所有用户  
- 所有用户及权限信息存储在mysql数据库的user表中  
- 查看user表的结构  
```SQL
desc user;
```

* 主要字段说明：  
 * Host表示允许访问的主机  
 * User表示用户名  
 * authentication_string表示密码，为加密后的值  
 
查看所有用户
```SQL
select host,user,authentication_string from user;
```

结果  
```SQL
mysql> select host,user,authentication_string from user;
+-----------+------------------+-------------------------------------------+
| host      | user             | authentication_string                     |
+-----------+------------------+-------------------------------------------+
| localhost | root             | *E74858DB86EBA20BC33D0AECAE8A8108C56B17FA |
| localhost | mysql.sys        | *THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE |
| localhost | debian-sys-maint | *EFED9C764966EDB33BB7318E1CBD122C0DFE4827 |
+-----------+------------------+-------------------------------------------+
3 rows in set (0.00 sec)
```

## 2. 创建账户、授权  
* 需要使用实例级账户登录后操作，以root为例  
* 常用权限主要包括：create、alter、drop、insert、update、delete、select  
* 如果分配所有权限，可以使用all privileges  

### 2.1 创建账户&授权
```SQL
grant 权限列表 on 数据库 to '用户名'@'访问主机' identified by '密码';
```


### 2.2 示例1  
创建一个`laowang`的账号，密码为123456，只能通过本地访问, 并且只能对jing_dong数据库中的所有表进行读操作

step1：使用root登录
```SQL
mysql -uroot -p
回车后写密码，然后回车
```
### step2：创建账户并授予所有权限  
```SQL
grant select on jing_dong.* to 'laowang'@'localhost' identified by '123456';
```

说 明  
 * 可以操作python数据库的所有表，方式为:jing_dong.*  
 * 访问主机通常使用 百分号% 表示此账户可以使用任何ip的主机登录访问此数据库  
 * 访问主机可以设置成 localhost或具体的ip，表示只允许本机或特定主机访问  
 
 * 查看用户有哪些权限  
```SQL
show grants for laowang@localhost;
```

step3：退出root的登录  
```SQL
quit
```

### step4：使用laowang账户登录  
```SQL
mysql -ulaowang -p
回车后写密码，然后回车
```

* 登录后效果如下图  

## 2.3 示例2
创建一个laoli的账号，密码为12345678，可以任意电脑进行链接访问, 并且对jing_dong数据库中的所有表拥有所有权限  
```SQL
grant all privileges on jing_dong.* to "laoli"@"%" identified by "12345678"  
```
