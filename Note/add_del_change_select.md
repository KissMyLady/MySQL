增-删-改-查 
====


## 增删改查(curd)  
curd的解释: 代表创建（Create）、更新（Update）、读取（Retrieve）和删除（Delete）  

## 查 询  
```SQL
select * from 表名;
例：
select * from classes;
```

查询指定列
可以使用as为列或表指定别名
```SQL
select 列1,列2,... from 表名;
例：
select id,name from classes;
```

## 增 加  
> 格式:INSERT [INTO] tb_name [(col_name,...)] {VALUES | VALUE} ({expr | DEFAULT},...),(...),...

- 说明：主键列是自动增长，但是在全列插入时需要占位，通常使用0或者 default 或者 null 来占位，插入成功后以实际数据为准
- 全列插入：值的顺序与表中字段的顺序对应  
```SQL
insert into 表名 values(...)
例：
insert into students values(0,’郭靖‘,1,'蒙古','2016-1-2');
```
- 部分列插入：值的顺序与给出的列顺序对应  
```SQL
insert into 表名(列1,...) values(值1,...)
例：
insert into students(name,hometown,birthday) values('黄蓉','桃花岛','2016-3-2');
```
- 上面的语句一次可以向表中插入一行数据，还可以一次性插入多行数据，这样可以减少与数据库的通信
- 全列多行插入：值的顺序与给出的列顺序对应
```SQL
insert into 表名 values(...),(...)...;
例：
insert into classes values(0,'python1'),(0,'python2');
```
```SQL
insert into 表名(列1,...) values(值1,...),(值1,...)...;
例：
insert into students(name) values('杨康'),('杨过'),('小龙女');
```

## 修 改  
> 格式: UPDATE tbname SET col1={expr1|DEFAULT} [,col2={expr2|default}]...[where 条件判断]
```SQL
update 表名 set 列1=值1,列2=值2... where 条件
例：
update students set gender=0,hometown='北京' where id=5;
```

## 删 除
> DELETE FROM tbname [where 条件判断]
```SQL
delete from 表名 where 条件
例：
delete from students where id=5;
```
- 逻辑删除，本质就是修改操作
```SQL
update students set isdelete=1 where id=1;
```
