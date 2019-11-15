备份与恢复  
====

## 备份  
- 运行mysqldump命令  
```SQL
mysqldump –uroot –p 数据库名 > python.sql;  

# 按提示输入mysql的密码
```

## 恢复  
- 连接mysql，创建新的数据库   
- 退出连接，执行如下命令  
```SQL
mysql -uroot –p 新数据库名 < python.sql  

# 根据提示输入mysql密码  
```
