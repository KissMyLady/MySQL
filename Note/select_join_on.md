SQL中的合并表查询  
=====

## 连接查询  
当查询结果的列来源于多张表时，需要将多张表连接成一个大的数据集，再选择合适的列返回  

mysql支持三种类型的连接查询，分别为：  

- 内连接查询：查询的结果为两个表匹配到的数据  
![]()  

  * 右连接查询：查询的结果为两个表匹配到的数据，右表特有的数据，对于左表中不存在的数据使用null填充  
![]() 

  * 左连接查询：查询的结果为两个表匹配到的数据，左表特有的数据，对于右表中不存在的数据使用null填充  
![]() 
  

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
