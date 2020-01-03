---

layout: post 
title: "Yarn Kerberos授权" 
date: 2019-10-23 10:00:00 +0800
categories: BigData
---


## 准备工作

### 服务器列表

|服务器IP|服务器作用|
|----------|----------------------------------------|
|172.17.0.5|KDC|



## Kerberos安装与配置

安装参考Hadoop相关章节


## 配置Hbase

### 配置环境变量
所有的环境配置

```shell
export JAVA_HOME=/usr/java/jdk1.8.0_45
export HBASE_HOME=/usr/local/hbase/
export PATH=$PATH:$JAVA_HOME/bin
export PATH=$PATH:$HBASE_HOME/bin
```

### YARN ResourceManager

配置yarn-site.xml

```html
<property>
    <name>yarn.resourcemanager.webapp.spnego-keytab-file</name>
    <value>/etc/security/keytabs/spnego.service.keytab</value>
</property>
<property>
    <name>yarn.resourcemanager.webapp.spnego-principal</name>
    <value>HTTP/10-241-10-109@EXAMPLE.COM</value>
</property>

```


