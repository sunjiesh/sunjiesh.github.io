---

layout: post 
title: "Spark Demo" 
date: 2019-12-20 00:00:00 +0800
categories: BigData
---

### Spark执行hive查询

```java
SparkSession sparkSession = SparkSession.builder().appName(appName)
                    .config("spark.sql.warehouse.dir", "/user/hive/warehouse")
                    .config("hive.metastore.uris", hiveMetastoreUris).enableHiveSupport().getOrCreate();    
String sql = "sql";
Dataset<Row> rowDatas = sparkSession.sqlContext().sql(sql);
```


