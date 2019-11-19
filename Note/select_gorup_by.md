数据库的分组查询  
=====

## 分组  
## group by
- 1、group by的含义:将查询结果按照1个或多个字段进行分组，字段值相同的为一组；  
- 2、group by可用于单个字段分组，也可用于多个字段分组；  
```SQL
select * from students;
+----+-----------+------+--------+--------+--------+-----------+
| id | name      | age  | height | gender | cls_id | is_delete |
+----+-----------+------+--------+--------+--------+-----------+
|  1 | 小明      |   18 | 180.00 | 女     |      1 |           |
|  2 | 小月月    |   18 | 180.00 | 女     |      2 |          |
|  3 | 彭于晏    |   29 | 185.00 | 男     |      1 |           |
|  4 | 刘德华    |   59 | 175.00 | 男     |      2 |          |
|  5 | 黄蓉      |   38 | 160.00 | 女     |      1 |           |
|  6 | 凤姐      |   28 | 150.00 | 保密   |      2 |          |
|  7 | 王祖贤    |   18 | 172.00 | 女     |      1 |          |
|  8 | 周杰伦    |   36 |   NULL | 男     |      1 |           |
|  9 | 程坤      |   27 | 181.00 | 男     |      2 |           |
| 10 | 刘亦菲    |   25 | 166.00 | 女     |      2 |           |
| 11 | 金星      |   33 | 162.00 | 中性   |      3 |          |
| 12 | 静香      |   12 | 180.00 | 女     |      4 |           |
| 13 | 周杰      |   34 | 176.00 | 女     |      5 |           |
| 14 | 郭靖      |   12 | 170.00 | 男     |      4 |           |
+----+-----------+------+--------+--------+--------+-----------+

select gender from students group by gender;
+--------+
| gender |
+--------+
| 男     |
| 女     |
| 中性   |
| 保密   |
+--------+
```
根据gender字段来分组，gender字段的全部值有4个'男','女','中性','保密'，所以分为了4组,   
当group by单独使用时，只显示出每组的第一条记录, 所以group by单独使用时的实际意义不大  


## group by + group_concat()  
- 1、group_concat(字段名)可以作为一个输出字段来使用，  
- 2、表示分组之后，根据分组结果，使用group_concat()来放置每一组的某字段的值的集合  
```SQL
select gender from students group by gender;
+--------+
| gender |
+--------+
| 男     |
| 女     |
| 中性   |
| 保密   |
+--------+

select gender,group_concat(name) from students group by gender;
+--------+-----------------------------------------------------------+
| gender | group_concat(name)                                        |
+--------+-----------------------------------------------------------+
| 男     | 彭于晏,刘德华,周杰伦,程坤,郭靖                                 |
| 女     | 小明,小月月,黄蓉,王祖贤,刘亦菲,静香,周杰                        |
| 中性   | 金星                                                       |
| 保密   | 凤姐                                                       |
+--------+-----------------------------------------------------------+

select gender,group_concat(id) from students group by gender;
+--------+------------------+
| gender | group_concat(id) |
+--------+------------------+
| 男     | 3,4,8,9,14       |
| 女     | 1,2,5,7,10,12,13 |
| 中性   | 11               |
| 保密   | 6                |
+--------+------------------+
```

## group by + 集合函数  
- 通过group_concat()的启发，我们既然可以统计出每个分组的某字段的值的集合，那么我们也可以通过集合函数来对这个值的集合做一些操作  
```SQL
select gender,group_concat(age) from students group by gender;
+--------+----------------------+
| gender | group_concat(age)    |
+--------+----------------------+
| 男     | 29,59,36,27,12       |
| 女     | 18,18,38,18,25,12,34 |
| 中性   | 33                   |
| 保密   | 28                   |
+--------+----------------------+

分别统计性别为男/女的人年龄平均值
select gender,avg(age) from students group by gender;
+--------+----------+
| gender | avg(age) |
+--------+----------+
| 男     |  32.6000 |
| 女     |  23.2857 |
| 中性   |  33.0000 |
| 保密   |  28.0000 |
+--------+----------+

分别统计性别为男/女的人的个数
select gender,count(*) from students group by gender;
+--------+----------+
| gender | count(*) |
+--------+----------+
| 男     |        5 |
| 女     |        7 |
| 中性   |        1 |
| 保密   |        1 |
+--------+----------+
```

## group by + having  
- 1、having 条件表达式：用来分组查询后指定一些条件来输出查询结果  
- 2、having作用和where一样，但having只能用于group by  
```SQL
select gender,count(*) from students group by gender having count(*)>2;
+--------+----------+
| gender | count(*) |
+--------+----------+
| 男     |        5 |
| 女     |        7 |
+--------+----------+
```

## group by + with rollup  
- with rollup的作用是：在最后新增一行，来记录当前列里所有记录的总和  
```SQL
select gender,count(*) from students group by gender with rollup;
+--------+----------+
| gender | count(*) |
+--------+----------+
| 男     |        5 |
| 女     |        7 |
| 中性   |        1 |
| 保密   |        1 |
| NULL   |       14 |
+--------+----------+

select gender,group_concat(age) from students group by gender with rollup;
+--------+-------------------------------------------+
| gender | group_concat(age)                         |
+--------+-------------------------------------------+
| 男     | 29,59,36,27,12                            |
| 女     | 18,18,38,18,25,12,34                      |
| 中性   | 33                                        |
| 保密   | 28                                        |
| NULL   | 29,59,36,27,12,18,18,38,18,25,12,34,33,28 |
+--------+-------------------------------------------+
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




















