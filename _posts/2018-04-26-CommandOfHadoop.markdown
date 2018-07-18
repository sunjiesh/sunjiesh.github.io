---

layout: post 
title: "Hadoop常用命令" 
date: 2018-04-13 10:00:00 +0800
categories: BigData
---

<pre>
  <code>$HADOOP_HOME/bin/hdfs namenode -format </code>
</pre>

启动NameNode(HDFS用户启动)
<pre>
  <code>$HADOOP_HOME/bin/hdfs --daemon start namenode</code>
</pre>
启动SecondaryNameNode(HDFS用户启动)
<pre>
  <code>$HADOOP_HOME/bin/hdfs --daemon start secondarynamenode</code>
</pre>

启动DataNode(HDFS用户启动)
<pre>
  <code>$HADOOP_HOME/bin/hdfs --daemon start datanode </code>
</pre>

启动resourcemanager(yarn用户启动)
<pre>
  <code>$HADOOP_HOME/bin/yarn --daemon start resourcemanager
 </code>
</pre>
启动nodemanager(yarn用户启动)
<pre>
  <code>$HADOOP_HOME/bin/yarn --daemon start nodemanager </code>
</pre>

启动proxyserver
<pre>
  <code>$HADOOP_HOME/bin/yarn --daemon start proxyserver </code>
</pre>

启动yarn
<pre>
  <code>$HADOOP_HOME/sbin/start-yarn.sh </code>
</pre>

清理HDFS回收箱
<pre>
  <code>$HADOOP_HOME/bin/hdfs dfs -expunge </code>
</pre>
