---

layout: post 
title: "Deploy Yarn" 
date: 2018-04-13 10:00:00 +0800
categories: BigData
---

配置环境变量

<pre>
  <code>export YARN_RESOURCEMANAGER_USER="root"export YARN_NODEMANAGER_USER="root"</code>
</pre>

修改配置文件 vim mapred-site.xml

```html
<property>
  <name>mapreduce.framework.name</name>
  <value>yarn</value>
</property>

```

vim yarn-site.xml

```html
<property>
  <name>yarn.nodemanager.local-dirs</name>
  <value>/data/hadoop_dir/temp/</value>
</property>
<property>
  <name>yarn.nodemanager.log-dirs</name>
  <value>/data/hadoop_dir/logs/</value>
</property>
<property>
  <name>yarn.log-aggregation-enable</name>
  <value>false</value>
</property>
<property>
  <name>yarn.nodemanager.pmem-check-enabled</name>
  <value>false</value>
</property>
<property>
  <name>yarn.nodemanager.vmem-check-enabled</name>
  <value>false</value>
</property>
<property>
  <name>yarn.resourcemanager.address</name>
  <value>${resourcemanagerip}:8032</value>
</property>
<property>
  <name>yarn.resourcemanager.scheduler.address</name>
  <value>${resourcemanagerip}:8030</value>
</property>
<property>
  <name>yarn.resourcemanager.resource-tracker.address</name>
  <value>${resourcemanagerip}:8031</value>
</property>

```

啟動服務

<pre>
  <code>
  $HADOOP_HOME/bin/yarn --daemon start resourcemanager 
  $HADOOP_HOME/bin/yarn --daemon start nodemanager
  </code>
</pre>
