一表多用--自关联  
====

## 自关联  
* 设计省信息的表结构provinces  
  * id
  * ptitle
* 设计市信息的表结构citys  
  * id
  * ctitle
  * proid
* citys表的proid表示城市所属的省，对应着provinces表的id值  

## 问 题： 
> 能不能将两个表合成一张表呢？  

## 思 考： 
> 观察两张表发现，citys表比provinces表多一个列proid，其它列的类型都是一样的  

## 意 义： 
> 存储的都是地区信息，而且每种信息的数据量有限，没必要增加一个新表，或者将来还要存储区、乡镇信息，都增加新表的开销太大  

## 答案：  
> 定义表areas，结构如下
> * id
> * atitle
> * pid

## 说 明:  
- 因为省没有所属的省份，所以可以填写为null  
- 城市所属的省份pid，填写省所对应的编号id  
- 这就是自关联，表中的某一列，关联了这个表中的另外一列，但是它们的业务逻辑含义是不一样的，城市信息的pid引用的是省信息的id  
- 在这个表中，结构不变，可以添加区县、乡镇街道、村社区等信息  

## 创建areas表的语句如下：  
```SQL
create table areas(
    aid int primary key,
    atitle varchar(20),
    pid int
);
```
- 从sql文件中导入数据  
```SQL
source areas.sql;
```
- 查询一共有多少个省  
```SQL
select count(*) from areas where pid is null;
```

- 例1：查询省的名称为“山西省”的所有城市  
```SQL
select city.* from areas as city
inner join areas as province on city.pid=province.aid
where province.atitle='山西省';
```
- 例2：查询市的名称为“广州市”的所有区县  
```SQL
select dis.* from areas as dis
inner join areas as city on city.aid=dis.pid
where city.atitle='广州市';
```

## 看完了  
- [返回MySQL主页](https://github.com/KissMyLady/MySQL/blob/master/README.md)
- [数据库的基本查询](https://github.com/KissMyLady/MySQL/blob/master/Note/select_from_databases1.md)  
- [数据库的条件查询](https://github.com/KissMyLady/MySQL/blob/master/Note/select_where.md)   
- [数据库的排序查询](https://github.com/KissMyLady/MySQL/blob/master/Note/select_order_by.md)  
- [SQL中的聚合函数](https://github.com/KissMyLady/MySQL/blob/master/Note/select_faction.md)  
- [数据库的分组查询](https://github.com/KissMyLady/MySQL/blob/master/Note/select_gorup_by.md)  
- [SQL中的limit方法](https://github.com/KissMyLady/MySQL/blob/master/Note/select_limit.md)  
- [SQL中的合并表查询](https://github.com/KissMyLady/MySQL/blob/master/Note/select_join_on.md)  
- [数据库的子查询](https://github.com/KissMyLady/MySQL/blob/master/Note/select_son_find.md) 








