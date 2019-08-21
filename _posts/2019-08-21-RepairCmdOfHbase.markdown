---

layout: post 
title: "Hbase修复命令" 
date: 2019-08-21 00:00:00 +0800
categories: BigData
---

示例
查看hbasemeta情况

```shell  
hbase hbck  
```
重新修复hbase meta表（根据hdfs上的regioninfo文件，生成meta表）  

```shell
hbase hbck -fixMeta  
```

重新将hbase meta表分给regionserver（根据meta表，将meta表上的region分给
regionservere）  

```shell
hbase hbck -fixAssignments  
```


### 引用 
[https://blog.csdn.net/liliwei0213/article/details/53639275](https://blog.csdn.net/liliwei0213/article/details/53639275).

