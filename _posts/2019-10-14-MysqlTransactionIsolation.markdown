---
layout: post
title:  "Mysql 隔离级别"
date:   2019-10-14 10:00:00 +0800
categories: Mysql
---

### 隔离级别
四种隔离级别如下（按照级别由低到高）：

#### read uncommitted（读未提交）
即使事务B没有commit，其它事务也能读取到事务B更新的数据，即能够读取事务没有提交的数据。这是事务隔离级别中等级最低的一个。

#### read committed（读已提交）
总结一下，在read committed（读已提交）级别时，其它事务只能读取事务B提交后的数据，未提交则读取不到。这是大部分数据库的默认隔离级别。

#### repeatable read（可重复读）
也就是说，当数据库处于repeatable read（可重复读）时，同一个事务前后两次所读取的数据必须是一致的，无论事务B有没有插入数据。它是MySQL的默认隔离级别。

#### Serializable（串行化）
Serializable（串行化）是等级最高，要求最严的事务隔离级别，在这种情况下，其它事务必须等待当前事务commit后才能执行。

### 引用

[https://mp.weixin.qq.com/s/p32Tc6XhbHq_NbJWAiZnhQ](https://mp.weixin.qq.com/s/p32Tc6XhbHq_NbJWAiZnhQ)