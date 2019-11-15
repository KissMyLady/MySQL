SQL中的合并表查询  
=====

## 连接查询  
当查询结果的列来源于多张表时，需要将多张表连接成一个大的数据集，再选择合适的列返回  

mysql支持三种类型的连接查询，分别为：  

  * 内连接查询：查询的结果为两个表匹配到的数据  
![1](https://github.com/KissMyLady/MySQL/blob/master/Img/join_on1.png)  

  * 右连接查询：查询的结果为两个表匹配到的数据，右表特有的数据，对于左表中不存在的数据使用null填充  
![2](https://github.com/KissMyLady/MySQL/blob/master/Img/join_on2.png) 

  * 左连接查询：查询的结果为两个表匹配到的数据，左表特有的数据，对于右表中不存在的数据使用null填充  
![3](https://github.com/KissMyLady/MySQL/blob/master/Img/join_on32.png) 
  

## 语 法  
```SQL
select * from 表1 inner或left或right join 表2 on 表1.列 = 表2.列
```
例1：使用内连接查询班级表与学生表
```SQL
select * from students inner join classes on students.cls_id = classes.id;
```
例2：使用左连接查询班级表与学生表
- 此处使用了as为表起别名，目的是编写简单
```SQL
select * from students as s left join classes as c on s.cls_id = c.id;
```
例3：使用右连接查询班级表与学生表
```SQL
select * from students as s right join classes as c on s.cls_id = c.id;
```
例4：查询学生姓名及班级名称
```SQL
select s.name,c.name from students as s inner join classes as c on s.cls_id = c.id;
```

## 看完了  
- [返回MySQL主页](https://github.com/KissMyLady/MySQL/blob/master/README.md)
- [数据库的基本查询](https://github.com/KissMyLady/MySQL/blob/master/Note/select_from_databases1.md)  
- [数据库的条件查询](https://github.com/KissMyLady/MySQL/blob/master/Note/select_where.md)   
- [数据库的排序查询](https://github.com/KissMyLady/MySQL/blob/master/Note/select_order_by.md)  
- [SQL中的聚合函数](https://github.com/KissMyLady/MySQL/blob/master/Note/select_faction.md)  
- [数据库的分组查询](https://github.com/KissMyLady/MySQL/blob/master/Note/select_gorup_by.md)  
- [SQL中的limit方法](https://github.com/KissMyLady/MySQL/blob/master/Note/select_limit.md)  
- [一表多用--自关联](https://github.com/KissMyLady/MySQL/blob/master/Note/select_self_knot.md)  
- [数据库的子查询](https://github.com/KissMyLady/MySQL/blob/master/Note/select_son_find.md) 
