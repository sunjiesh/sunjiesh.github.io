---

layout: post 
title: "安装Hive" 
date: 2018-05-24 10:00:00 +0800
categories: BigData
---

## 准备环境


### 创建用户

```shell
useradd hive -g hadoop
```

### 环境变量

```shell
export HDFS_NAMENODE_USER="hdfs"
export HDFS_DATANODE_USER="hdfs"
export HDFS_SECONDARYNAMENODE_USER="hdfs"
export YARN_RESOURCEMANAGER_USER="yarn"
export YARN_NODEMANAGER_USER="yarn"

export HADOOP_CONF_DIR=/data/hadoop-install/etc/hadoop
export JAVA_HOME=/usr/java/jdk1.8.0_45
export HBASE_HOME=/usr/local/hbase/
export HADOOP_HOME=/data/hadoop-install
export HIVE_HOME=/data/hive-install
export PATH=$PATH:$JAVA_HOME/bin
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
export PATH=$PATH:$HIVE_HOME/bin
```

## 安装与配置

### 安装Hive-Server2

#### 修改hive-site.xml

vim hive-site.xml

```shell
<configuration>
    <property>
      <name>javax.jdo.option.ConnectionURL</name>
      <value>jdbc:mysql://mysqlip:3306/hive?createDatabaseIfNotExist=true</value>
    </property>
    <property>
      <name>javax.jdo.option.ConnectionDriverName</name>
      <value>com.mysql.jdbc.Driver</value>
    </property>
    <property>
      <name>javax.jdo.option.ConnectionUserName</name>
      <value>root</value>
    </property>
    <property>
      <name>javax.jdo.option.ConnectionPassword</name>
      <value>123456</value>
    </property>
    
    <property>  
	    <name>hive.server2.enable.doAs</name>  
	    <value>false</value>  
	</property>
</configuration>
```
javax.jdo.option 配置元数据数据库连接信息
hive.server2.enable.doAs 需要设置为false


#### 初始化

需要把mysql-connector-java-x.y.z.jar包放入$HIVE_HOME/lib/目录中

```shell
cp /tmp/mysql-connector-java-5.1.26.jar $HIVE_HOME/lib/
$HIVE_HOME/bin/schematool -dbType mysql -initSchema
```

正确结果返回如下

```shell
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/data/hive-install/lib/log4j-slf4j-impl-2.6.2.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/data/hadoop-install/share/hadoop/common/lib/slf4j-log4j12-1.7.25.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.apache.logging.slf4j.Log4jLoggerFactory]
Metastore connection URL:	 jdbc:mysql://10.241.10.108:3306/hive?createDatabaseIfNotExist=true
Metastore Connection Driver :	 com.mysql.jdbc.Driver
Metastore connection User:	 root
Starting metastore schema initialization to 2.3.0
Initialization script hive-schema-2.3.0.mysql.sql
Initialization script completed
schemaTool completed
```

#### 启动

```shell
$HIVE_HOME/bin/hive --service hiveserver2
```

## 引用：

<a href="https://stackoverflow.com/questions/40077938/access-hbase-with-hiveserver2-error?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa" target="_blank">https://stackoverflow.com/questions/40077938/access-hbase-with-hiveserver2-error?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa</a>

