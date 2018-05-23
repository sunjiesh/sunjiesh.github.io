---

layout: post 
title: "Spark读取Hbase错误" 
date: 2018-05-23 10:00:00 +0800
categories: BigData
---

特意把折腾了好几天的问题列下来，供以后检阅

## java.lang.IllegalStateException: unread block data

根据网上找的方法，说是因为版本兼容问题导致的，经过设置了hbase-client、hadoop-client版本，发现都不行。后来无意中在spark-env.sh设置了SPARK_CLASSPATH变量，把Hbase的classpath放入SPARK_CLASSPATH中，居然就成功了，具体原因未知。

参考方法：
https://github.com/GenTang/spark_hbase/blob/master/README.md
