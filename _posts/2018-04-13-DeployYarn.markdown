---

layout: post 
title: "Deploy Yarn" 
date: 2018-04-13 10:00:00 +0800
categories: BigData
---


## 前置条件

### 安装Hadoop
参考对应相关文档

### 配置环境变量


```shell

export YARN_RESOURCEMANAGER_USER="yarn"
export YARN_NODEMANAGER_USER="yarn"

export JAVA_HOME=/usr/java/jdk1.8.0_45
export HADOOP_HOME=/data/hadoop-install
export HADOOP_CONF_DIR=/data/hadoop-install/etc/hadoop
export PATH=$PATH:$JAVA_HOME/bin
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin

```

如果不设置HADOOP\_CONF\_DIR会导致找不到相关配置文件，导致报错

## 配置HADOOP

### 修改mapred-site.xml

```html
<property>
  <name>mapreduce.framework.name</name>
  <value>yarn</value>
</property>

```

### 修改yarn-site.xml

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

## 启动服务与验证

### 啟動服務

```shell
  $HADOOP_HOME/bin/yarn --daemon start resourcemanager 
  $HADOOP_HOME/bin/yarn --daemon start nodemanager
```

### 验证
通过JPS命令查询服务是否正常

```shell
18372 ResourceManager
18888 Jps
18734 NodeManager
```

