---
title: mysql索引初探
date: 2019-12-20 16:13:27
categories: 
- [数据库]
---

> 前段时间写了一个流程中心，因时间紧张且上线初期数据不多，没有过多关注数据库方面的优化，近期准备优化。  
目标支撑1千万的数据量原测试代码在10秒内跑完。  
故准备学习mysql优化并记录项目优化改造过程。
<!--more-->

```sql
# 数据
# 7000000
select  *  from TEST_SQL_A  where sys_id = 'D'; # 1.62

select  *  from TEST_SQL_A  where sys_id = 'D' order by time limit 900000,10; # 3.56

# 对 sys_id 加索引
select  count(*)  from TEST_SQL_A  where sys_id = 'D'; # 498

select  *  from TEST_SQL_A  where sys_id = 'D' order by time limit 900000,10; # 5.36

# 对 time 加索引
explain select  *  from TEST_SQL_A  where sys_id = 'D'; # 498

select  *  from TEST_SQL_A  where sys_id = 'D' order by time limit 900000,10; # 5.36

select  *  from TEST_SQL_A  order by time desc limit 900000,10; # 3.853

# 为什么加了索引没用
select  *  from TEST_SQL_A  order by time desc limit 900000,10;

select  *  from TEST_SQL_A  order by id limit 1900000,10; # 439

explain select  id  from TEST_SQL_A  order by id limit 1900000,10; # 284

select count(*) from TEST_SQL_A;
select * from TEST_SQL_A where id = 6700000; #55

# 改为 9000 无time 索引
select  *  from TEST_SQL_A  order by time desc limit 9000,10; # 2.84

select  *  from TEST_SQL_A  where sys_id = 'D' order by time limit 100,10; # 5.36

# 加time 索引
select  *  from TEST_SQL_A  order by time desc limit 9000,10; # 68

select  *  from TEST_SQL_A  where sys_id = 'D' order by time limit 100,10; # 5.36
# 索引可以控制排序但是没有统计数量，offset 过大效率的，不会走索引

# 加sys_id 加time 索引
select  *  from TEST_SQL_A  order by time desc limit 9000,10; # 68

select  *  from TEST_SQL_A  where sys_id = 'D' order by time limit 19000,10; # 67

select  *  from TEST_SQL_A  where sys_id = 'D'
            and time > str_to_date('2019-12-20 10:30', '%Y-%m-%d %H:%i') order by time limit 9000,10; # 78

# 总结 offset 过大任何索引都会大幅降低效率包括主键，但应用不会出现大的offset， 如上9000加上索引查询速度非常快，而且完全够应用使用
#

# D 1560 共 18300000
# 无索引
select count(*) from TEST_SQL_B b1 join TEST_SQL_A a1 on a1.ID = b1.ID where b1.sys_id = 'D'; # 3.440
select count(*) from TEST_SQL_A a1 join TEST_SQL_B b1 on a1.ID = b1.ID where b1.sys_id = 'D'; # 3.440

select count(*) from TEST_SQL_B b1 join TEST_SQL_A a1 on a1.ID = b1.ID where b1.sys_id = 'A'; # 15.64
# 加了sys_id time 联合索引
select count(*) from TEST_SQL_B b1 join TEST_SQL_A a1 on a1.ID = b1.ID where b1.sys_id = 'D'; # 47
select * from TEST_SQL_B b1 join TEST_SQL_A a1 on a1.ID = b1.ID where b1.sys_id = 'D'; # 47
select count(*) from TEST_SQL_A a1 join TEST_SQL_B b1 on a1.ID = b1.ID where b1.sys_id = 'D'; # 50

select count(*) from TEST_SQL_B b1 join TEST_SQL_A a1 on a1.ID = b1.ID where b1.sys_id = 'A'; # 10.64

select * from TEST_SQL_A a1;

# 索引与字段属性关系，字段大，单个索引所需空闲大，页数变多

```