SQL中的聚合函数  
====

## 聚合函数  
为了快速得到统计数据，经常会用到如下5个聚合函数  

## 总 数  
- count(*)表示计算总行数，括号中写星与列名，结果是相同的  
例1：查询学生总数  
```SQL
select count(*) from students;
```

## 最大值  
- max(列)表示求此列的最大值  
例2：查询女生的编号最大值  
```SQL
select max(id) from students where gender=2; 
```

## 最小值  
- min(列)表示求此列的最小值  
例3：查询未删除的学生最小编号  
```SQL
select min(id) from students where is_delete=0;
```

## 求 和  
- sum(列)表示求此列的和
例4：查询男生的总年龄
```SQL
select sum(age) from students where gender=1;
-- 平均年龄
select sum(age)/count(*) from students where gender=1;
```

## 平均值  
- avg(列)表示求此列的平均值  
例5：查询未删除女生的编号平均值  
```SQL
select avg(id) from students where is_delete=0 and gender=2;
```
