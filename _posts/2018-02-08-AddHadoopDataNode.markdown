---
layout: post
title:  "Add new hadoop datanode"
date:   2018-02-08 10:00:00 +0800
categories: Linux
---

主要流程
### 新DataNode配置环境变量

### 新DataNode配置SSH免密登录

```shell
cat id_rsa.pub >> authorized_keys
cat id_rsa_hadoop_namenode.pub >> authorized_keys
```

### 配置DataNode

```shell
在新DataNode分别配置core-site.xml和hdfs-site.xml
```

### 配置NameNode

```shell
配置NameNode的etc/hadoop/workers文件
```

### 新DataNode上执行

```shell
hadoop-daemon.sh start datanode
```

### 检查 

```shell
hdfs dfsadmin -report
```
