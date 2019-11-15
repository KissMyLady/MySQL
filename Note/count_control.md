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

## 2.3 示例2
创建一个laoli的账号，密码为12345678，可以任意电脑进行链接访问, 并且对jing_dong数据库中的所有表拥有所有权限  
```SQL
grant all privileges on jing_dong.* to "laoli"@"%" identified by "12345678"  
```

# 账户操作  
## 1. 修改权限    
```SQL
grant 权限名称 on 数据库 to 账户@主机 with grant option;
```


## 2. 修改密码  
使用root登录，修改mysql数据库的user表  

- 使用password()函数进行密码加密  
```SQL
update user set authentication_string=password('新密码') where user='用户名';  

例：  
update user set authentication_string=password('123') where user='laowang'; 
```
1 注意修改完成后需要刷新权限  
```SQL
刷新权限：flush privileges  
 ```
 
## 3. 远程登录（危险慎用）  
如果向在一个Ubuntu中使用msyql命令远程连接另外一台mysql服务器的话，通过以下方式即可完成，但是此方法仅仅了解就好了，不要在实际生产环境中使用

修改 /etc/mysql/mysql.conf.d/mysqld.cnf 文件  
```SQL
vim /etc/mysql/mysql.conf.d/mysqld.cnf
```
![count1](https://github.com/KissMyLady/MySQL/blob/master/Img/count_contrl1.png)  

然后重启msyql  
```SQL
service mysql restart  
```

在另外一台Ubuntu中进行连接测试  
![count2](https://github.com/KissMyLady/MySQL/blob/master/Img/count_1.png)  

如果依然连不上，可能原因：  

1) 网络不通

> 通过 ping xxx.xxx.xx.xxx可以发现网络是否正常  

2)查看数据库是否配置了bind_address参数  

> 本地登录数据库查看my.cnf文件和数据库当前参数show variables like 'bind_address';  

> 如果设置了bind_address=127.0.0.1 那么只能本地登录  

3)查看数据库是否设置了skip_networking参数  

? 如果设置了该参数，那么只能本地登录mysql数据库  

4)端口指定是否正确  


## 4. 删除账户  
- 语法1：使用root登录  
```SQL
drop user '用户名'@'主机';
例：
drop user 'laowang'@'%';
```

- 语法2：使用root登录，删除mysql数据库的user表中数据
```SQL
delete from user where user='用户名';
例：
delete from user where user='laowang';

-- 操作结束之后需要刷新权限
flush privileges
```
- 推荐使用语法1删除用户, 如果使用语法1删除失败，采用语法2方式

## 3. 忘记 root 账户密码怎么办 !!  
一般也轮不到我们来管理 root 账户,所以别瞎卖白粉的心了  
万一呢? 到时候再来查http://blog.csdn.net/lxpbs8851/article/details/10895085  
```SQL
skip-grant-tables
顾名思义，数据库启动的时候 跳跃权限表的限制，不用验证密码，直接登录。

注意：

这种情况只有在忘记root密码 不得已重启数据库的情况下使用的。现网环境慎用，需要重启数据库，并且安全性也比较难以保证。

1.修改配置参数

/etc/my.cnf

在

[mysqld] 下面加上:

skip-grant-tables
配置项。

2.重启mysql

使得参数生效：

service mysqld restart

3.注意事项

此时所有用户登录当前数据库都是免密码的，所以此时数据库的安全性是非常低的。

4.修改密码

具体的办法：

   1.密码的初始化

   刚安装好的mysql root 的密码默认的空的

   /app/mysql/ 为mysql的安装目录。

   先执行：

   /app/mysql/bin/mysqladmin -u root password  test_password

   然后登陆mysql

   mysql -uroot -ptest_password

   执行：

   mysql>flush privileges;



   2.修改密码方法一

   /app/mysql/bin/mysqladmin -uroot -ptest_password   password new_password

   然后登陆mysql

   mysql -uroot -pnew_password

   执行：

   mysql>flush privileges;



   3.修改密码方法二

   然后登陆mysql

   mysql -uroot -pnew_password

   mysql> update mysql.user set password=password('test_new2_password') where user= 'root';
       mysql> FLUSH PRIVILEGES;


5.去掉参数

a.密码修改好了之后再将配置文件中 skip-grant-tables去掉

b.再次重启数据库。
```

