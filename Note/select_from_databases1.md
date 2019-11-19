数据库的基本查询  
====

## 查询所有字段  
```SQL
select * from 表名;
例：
select * from students;
```

## 查询指定字段  
```SQL
select 列1,列2,... from 表名;
例:
select name from students;
```
## 使用 as 给字段起别名  
```SQL
select id as 序号, name as 名字, gender as 性别 from students;

- 可以通过 as 给表起别名
-- 如果是单表查询 可以省略表明
select id, name, gender from students;

-- 表名.字段名
select students.id,students.name,students.gender from students;

-- 可以通过 as 给表起别名 
select s.id,s.name,s.gender from students as s;
```
 
## 消除重复行  
- 在select后面列前使用distinct可以消除重复的行  
```SQL
select distinct 列1,... from 表名;
例：
select distinct gender from students;
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


