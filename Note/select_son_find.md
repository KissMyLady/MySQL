数据库的子查询  
====

## 子查询  
> 在一个 select 语句中,嵌入了另外一个 select 语句, 那么被嵌入的 select 语句称之为子查询语句  

## 主查询  
> 主要查询的对象,第一条 select 语句  

## 主查询和子查询的关系    
> 子查询是嵌入到主查询中  
> 子查询是辅助主查询的,要么充当条件,要么充当数据源  
> 子查询是可以独立存在的语句,是一条完整的 select 语句  

## 子查询分类  
> 标量子查询: 子查询返回的结果是一个数据(一行一列)  
> 列子查询: 返回的结果是一列(一列多行)  
> 行子查询: 返回的结果是一行(一行多列)  

## 标量子查询  
1、查询班级学生平均年龄
2、查询大于平均年龄的学生
- 查询班级学生的平均身高
```SQL
select * from students where age > (select avg(age) from students);
```

## 列级子查询  
* 查询还有学生在班的所有班级名字
  * 1、找出学生表中所有的班级 id
  * 2、找出班级表中对应的名字
```SQL
select name from classes where id in (select cls_id from students);
```

## 行级子查询  
- 需求: 查找班级年龄最大,身高最高的学生
- 行元素: 将多个字段合成一个行元素,在行级子查询中会使用到行元素
```SQL
select * from students where (height,age) = (select max(height),max(age) from students);
```

## 子查询中特定关键字使用  
* in 范围
  * 格式: 主查询 where 条件 in (列子查询)

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
- [下一章：Python对数据库的基本操作](https://github.com/KissMyLady/MySQL/blob/master/Note/py_mysql1.md) 
