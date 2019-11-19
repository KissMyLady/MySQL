SQL中的limit方法  
====

## 获取部分行  
当数据量过大时，在一页中查看数据是一件非常麻烦的事情  

## 语法   
```SQL 
select * from 表名 limit start,count
```

## 说明  
从start开始，获取count条数据
例1：查询前3行男生信息
```SQL
select * from students where gender=1 limit 0,3;
```

## 示例：分页
* 已知：每页显示m条数据，当前显示第n页
* 求总页数：此段逻辑后面会在python中实现
  * 查询总条数p1
  * 使用p1除以m得到p2
  * 如果整除则p2为总数页
  * 如果不整除则p2+1为总页数
* 求第n页的数据
```SQL
select * from students where is_delete=0 limit (n-1)*m,m
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
