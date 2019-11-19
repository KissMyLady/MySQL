数据库的条件查询  
=====

## 条 件
使用where子句对表中的数据筛选，结果为true的行会出现在结果集中

- 语法如下： 
```SQL
select * from 表名 where 条件;
例：
select * from students where id=1;
``` 
* where后面支持多种运算符，进行条件的处理  
  * 比较运算符  
  * 逻辑运算符  
  * 模糊查询  
  * 范围查询  
  * 空判断  
  
## 比较运算符  
- =,  >,  >=,  <,  <=  
- 不等于: != 或 <>  

### 例1：查询编号大于3的学生  
```SQL
select * from students where id > 3;  
```
### 例2：查询编号不大于4的学生  
```SQL
select * from students where id <= 4;  
```
例3：查询姓名不是“黄蓉”的学生  
```SQL
select * from students where name != '黄蓉';
```
例4：查询没被删除的学生  
```SQL
select * from students where is_delete=0;
```

## 逻辑运算符  
and,  or,  not

例5：查询编号大于3的女同学  
```SQL
select * from students where id > 3 and gender=0;
```
例6：查询编号小于4或没被删除的学生  
```SQL
select * from students where id < 4 or is_delete=0;
```

## 模糊查询  
- like  
- %表示任意多个任意字符  
- _表示一个任意字符  

例7：查询姓黄的学生  
```SQL
select * from students where name like '黄%';
```
例8：查询姓黄并且“名”是一个字的学生  
```SQL
select * from students where name like '黄_';
```
例9：查询姓黄或叫靖的学生  
```SQL
select * from students where name like '黄%' or name like '%靖';
```

## 范围查询  
- in表示在一个非连续的范围内  
例10：查询编号是1或3或8的学生
```SQL
select * from students where id in(1,3,8);
```  
- between ... and ...表示在一个连续的范围内  

例11：查询编号为3至8的学生  
```SQL
select * from students where id between 3 and 8;
```  

例12：查询编号是3至8的男生  
```SQL
select * from students where (id between 3 and 8) and gender=1;
```  

## 空判断  
- 注意：null与''是不同的
- 判空is null

例13：查询没有填写身高的学生  
```SQL
select * from students where height is null;
```

- 判非空is not null
例14：查询填写了身高的学生
```SQL
select * from students where height is not null;
```
例15：查询填写了身高的男生
```SQL
select * from students where height is not null and gender=1;
```

## 优先级  
- 优先级由高到低的顺序为：小括号，not，比较运算符，逻辑运算符  
- and比or先运算，如果同时出现并希望先算or，需要结合()使用  


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



















