---

layout: post 
title: "hbase数据无法导入问题（org.apache.hadoop.hbase.NotServingRegionException: Region is not online）" 
date: 2019-07-09 00:00:00 +0800
categories: BigData
---

可先通过hbase hbck进行检查是否正常，一般会提示不一致（INCONSISTENT），一般方法为通过命令：hbase hbck -fix修复。修复成功状态为OK。 


### 引用 
[https://blog.csdn.net/qq_27078095/article/details/52671655](https://blog.csdn.net/qq_27078095/article/details/52671655).

