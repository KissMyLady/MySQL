数据库的排序查询  
=======

## 排 序  
为了方便查看数据，可以对数据进行排序  

## 语 法：
```SQL
select * from 表名 order by 列1 asc | desc [,列2 asc|desc,...]
 ```
 
## 说 明  
- 将行数据按照列1进行排序，如果某些行列1的值相同时，则按照列2排序，以此类推  
- 默认按照列值从小到大排列（asc）  
- asc从小到大排列，即升序  
- desc从大到小排序，即降序  

例1：查询未删除男生信息，按学号降序  
```SQL
select * from students where gender=1 and is_delete=0 order by id desc;  
```
例2：查询未删除学生信息，按名称升序  
```SQL
select * from students where is_delete=0 order by name;  
```
例3：显示所有的学生信息，先按照年龄从大-->小排序，当年龄相同时 按照身高从高-->矮排序  
```SQL
select * from students  order by age desc,height desc;  
```

## 看完了  
- [基本查询](https://github.com/KissMyLady/MySQL/blob/master/Note/select_from_databases1.md)  
- [条件](https://github.com/KissMyLady/MySQL/blob/master/Note/select_where.md)   
- [排序](https://github.com/KissMyLady/MySQL/blob/master/Note/select_order_by.md)  
- [聚合函数](https://github.com/KissMyLady/MySQL/blob/master/Note/select_faction.md)  
- [分组](https://github.com/KissMyLady/MySQL/blob/master/Note/select_gorup_by.md)  
- [分页](https://github.com/KissMyLady/MySQL/blob/master/Note/select_limit.md)  
- [连接表](https://github.com/KissMyLady/MySQL/blob/master/Note/select_join_on.md)  
- [一表多用--自关联](https://github.com/KissMyLady/MySQL/blob/master/Note/select_self_knot.md)  
- [子查询](https://github.com/KissMyLady/MySQL/blob/master/Note/select_son_find.md)  
- [数据库查询全总结](https://github.com/KissMyLady/MySQL/blob/master/Note/summary2.md) 
- [返回MySQL主页](https://github.com/KissMyLady/MySQL/blob/master/README.md)






