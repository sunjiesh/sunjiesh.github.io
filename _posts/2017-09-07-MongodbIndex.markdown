---
layout: post
title:  "Mongodb索引操作"
date:   2017-09-07 22:00:00 +0800
categories: Nosql
---
MongoDB的索引几乎与传统的关系型数据库一模一样，这其中也包括一些基本的优化技巧。下面是创建索引的命令：
> db.test.ensureIndex({"username":1})
可以通过下面的名称查看索引是否已经成功建立：
> db.test.getIndexes()
删除索引的命令是：
> db.test.dropIndex({"username":1})
在MongoDB中，我们同样可以创建复合索引，如： 数字1表示username键的索引按升序存储，-1表示age键的索引按照降序方式存储。
> db.test.ensureIndex({"username":1, "age":-1})
该索引被创建后，基于username和age的查询将会用到该索引，或者是基于username的查询也会用到该索引，但是只是基于age的查询将不会用到该复合索引。因此可以说，如果想用到复合索引，必须在查询条件中包含复合索引中的前N个索引列。然而如果查询条件中的键值顺序和复合索引中的创建顺序不一致的话，MongoDB可以智能的帮助我们调整该顺序，以便使复合索引可以为查询所用。如：
> db.test.find({"age": 30, "username": "stephen"})
对于上面示例中的查询条件，MongoDB在检索之前将会动态的调整查询条件文档的顺序，以使该查询可以用到刚刚创建的复合索引。
我们可以为内嵌文档创建索引，其规则和普通文档没有任何差别，如：
> db.test.ensureIndex({"comments.date":1})
对于上面创建的索引，MongoDB都会根据索引的keyname和索引方向为新创建的索引自动分配一个索引名，下面的命令可以在创建索引时为其指定索引名，如：
> db.test.ensureIndex({"username":1},{"name":"testindex"}) 
随着集合的增长，需要针对查询中大量的排序做索引。如果没有对索引的键调用sort，MongoDB需要将所有数据提取到内存并排序。因此在做无索引排序时，如果数据量过大以致无法在内存中进行排序，此时MongoDB将会报错。
