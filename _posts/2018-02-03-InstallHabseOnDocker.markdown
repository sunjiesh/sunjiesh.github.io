---
layout: post
title:  "Install hbase on docker"
date:   2018-02-03 10:00:00 +0800
categories: Linux
---

## 准备工作
### 分配
node1.example.com Hadoop
node2.example.com Zookeeper
node3.example.com HMaster HRegion

### Start docker 
执行命令
<pre>
docker run -i -t -d -v /data/docker/hadoop_node1_data:/data sunjie310110/hadoop
docker run -i -t -d -v /data/docker/hadoop_node2_data:/data sunjie310110/hadoop
docker run -i -t -d -v /data/docker/hadoop_node3_data:/data sunjie310110/hadoop
</pre>

### 设置Hosts文件
所有的机器上面都进行设置
<pre>
172.17.0.3      9aafd31815d4 node1.example.com
172.17.0.4      14eb4119a79f node2.example.com
172.17.0.5      c653e809297f node3.example.com
</pre>

### 配置环境变量
<pre>
export JAVA_HOME=/usr/jvm/jdk1.8.0_144
export HADOOP_HOME=/home/hadoop/hadoop
export HBASE_HOME=/home/hadoop/hbase
export ZOOKEEPER_HOME=/home/hadoop/zookeeper
export PATH=$PATH:$JAVA_HOME/bin
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
export PATH=$PATH:$HBASE_HOME/bin
export PATH=$PATH:$ZOOKEEPER_HOME/bin
</pre>

## Hadoop配置与启动
### 配置core-site.xml
执行如下命令进行编辑
<pre>
cd $HADOOP_HOME/etc/hadoop/
vim core-site.xml
</pre>
添加如下配置
<code>
<![CDATA[
<property>
<name>fs.defaultFS</name>
<value>hdfs://node1.example.com:9000</value>
</property>
]]>
</code>
fs.defaultFs一定设置域名，不能设置localhost，否则会导致hbase的hmaster无法启动

### 配置hdfs-site.xml
执行如下命令进行编辑
<pre>
cd $HADOOP_HOME/etc/hadoop/
vim hdfs-site.xml
</pre>
添加如下配置
<code>
<![CDATA[
<property>
<name>dfs.replication</name>
<value>3</value>
</property>
<property>
<name>dfs.name.dir</name>
<value>/data/hdfs/name</value>
</property>
<property>
<name>dfs.checkpoint.dir</name>
<value>/data/hdfs/namesecondary</value>
</property>
<property>
<name>dfs.data.dir</name>
<value>/data/hdfs/data</value>
</property>
]]>
</code>

### 格式化HDFS
执行命令
<code>
hdfs namenode -format
</code>

### 启动HDFS
执行命令
<code>
start-dfs.sh
</code>

### 验证启动完成
输入jps，出现NameNode、DataNode、SecondaryNameNode即表示成功
<code>
hadoop@9aafd31815d4:/tmp$ jps
1984 NameNode
2131 DataNode
2477 Jps
2333 SecondaryNameNode
</code>


## Zookeeper配置与启动
### 配置
修改默认配置文件
<code>
cd $ZOOKEEPER_HOME/conf
vim zoo.cfg
</code>
修改dataDir，改为指定目录，例如
<code>
dataDir=/data/zookeeper
</code>

### 启动
启动命令如下
<pre>
hadoop@14eb4119a79f:/home/hadoop/zookeeper/conf$ zkServer.sh start
ZooKeeper JMX enabled by default
Using config: /home/hadoop/zookeeper/bin/../conf/zoo.cfg
Starting zookeeper ... STARTED
</pre>

## Hbase配置与启动
### 配置hbase-site.xml
<property>
<name>hbase.rootdir</name>
<value>hdfs://node1.example.com:9000/hbase</value>
</property>
<property>
<name>hbase.zookeeper.quorum</name>
<value>node2.example.com</value>
</property>
<property>
<name>hbase.zookeeper.property.clientPort</name>
<value>2181</value>
</property>
<property>
<name>hbase.cluster.distributed</name>
<value>true</value>
</property>
### 配置 regionservers
删除原有记录，添加如下记录
<code>
node3.example.com
</code>
### 修改hbase-env.sh
添加如下命令
<code>
export HBASE_MANAGES_ZK=false
</code>
### 启动
<code>
hadoop@c653e809297f:/tmp$ start-hbase.sh 
running master, logging to /home/hadoop/hbase/logs/hbase-hadoop-master-c653e809297f.out
Java HotSpot(TM) 64-Bit Server VM warning: ignoring option PermSize=128m; support was removed in 8.0
Java HotSpot(TM) 64-Bit Server VM warning: ignoring option MaxPermSize=128m; support was removed in 8.0
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/home/hadoop/hbase/lib/slf4j-log4j12-1.7.10.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/home/hadoop/hadoop/share/hadoop/common/lib/slf4j-log4j12-1.7.25.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.slf4j.impl.Log4jLoggerFactory]
node3.example.com: running regionserver, logging to /home/hadoop/hbase/logs/hbase-hadoop-regionserver-c653e809297f.out
node3.example.com: Java HotSpot(TM) 64-Bit Server VM warning: ignoring option PermSize=128m; support was removed in 8.0
node3.example.com: Java HotSpot(TM) 64-Bit Server VM warning: ignoring option MaxPermSize=128m; support was removed in 8.0
</code>
### 验证启动完成
输入jps，出现HRegionServer和HMaster即表示成功
<code>
4644 HMaster
4827 HRegionServer
5197 Jps
</code>
