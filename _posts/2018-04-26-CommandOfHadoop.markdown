---

layout: post 
title: "Hadoop常用命令" 
date: 2018-04-13 10:00:00 +0800
categories: BigData
---

<pre>
  <code>$HADOOP_HOME/bin/hdfs namenode -format </code>
</pre>

启动NameNode
<pre>
  <code>$HADOOP_HOME/bin/hdfs --daemon start namenode</code>
</pre>

启动DataNode
<pre>
  <code>$HADOOP_HOME/bin/hdfs --daemon start datanode </code>
</pre>

启动resourcemanager
<pre>
  <code>$HADOOP_HOME/bin/yarn --daemon start resourcemanager
 </code>
</pre>
启动nodemanager
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
启动
<pre>
  <code> </code>
</pre>
