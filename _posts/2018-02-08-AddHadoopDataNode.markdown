---
layout: post
title:  "Add new hadoop datanode"
date:   2018-02-08 10:00:00 +0800
categories: Linux
---

主要流程
### 新DataNode配置环境变量

### 新DataNode配置SSH免密登录
<code>
cat id_rsa.pub >> authorized_keys
cat id_rsa_hadoop_namenode.pub >> authorized_keys
</code>

### 配置DataNode
<code>
在新DataNode分别配置core-site.xml和hdfs-site.xml
</code>

### 配置NameNode
<code>
配置NameNode的etc/hadoop/workers文件
</code>

### 新DataNode上执行
<code>
hadoop-daemon.sh start datanode
</code>

### 检查 
<code>
hdfs dfsadmin -report
</code>
