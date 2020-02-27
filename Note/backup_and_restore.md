备份与恢复  
====
数据全部导:     
```sql
mysqldump -uroot -pmysql --all-databases --lock-all-tables > ~/master_db.sql
```
数据全部导出实例2:       
```sql
mysqldump -uroot -pPASSWORD --all-databases --lock-all-tables > /home/master_db.sql
```
导 入:  
```sql
mysql –uroot –pPASSWORD < master_db.sql
```

### 备份  
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

## 看完了  
- [数据库的基本使用](https://github.com/KissMyLady/MySQL/edit/master/Note/base_use1.md)
- [基础-增删改查](https://github.com/KissMyLady/MySQL/blob/master/Note/add_del_change_select.md)
- [数据库备份与恢复](https://github.com/KissMyLady/MySQL/blob/master/Note/backup_and_restore.md)
- [数据库规范与设计](https://github.com/KissMyLady/MySQL/blob/master/Note/design_databases.md)
- [返回主页](https://github.com/KissMyLady/MySQL)
