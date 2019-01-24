---

layout: post 
title: "HIVE集成MR" 
date: 2018-12-19 10:00:00 +0800
categories: BigData
---

修改
/etc/hadoop/mapred-site.xml

```xml

<property>
  <name>yarn.app.mapreduce.am.env</name>
  <value>HADOOP_MAPRED_HOME=/usr/local/hadoop/etc/hadoop</value>
</property>
<property>
  <name>mapreduce.map.env</name>
  <value>HADOOP_MAPRED_HOME=/usr/local/hadoop/etc/hadoop</value>
</property>
<property>
  <name>mapreduce.reduce.env</name>
  <value>HADOOP_MAPRED_HOME=/usr/local/hadoop/etc/hadoop</value>
</property>


```
