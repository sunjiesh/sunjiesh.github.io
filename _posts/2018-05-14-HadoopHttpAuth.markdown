---

layout: post 
title: "Hadoop Http	认证" 
date: 2018-05-14 10:00:00 +0800
categories: BigData
---

# Hadoop Kerberos 授权（Http）

## 准备工作

### 服务器列表

|服务器IP---|服务器作用|
|----------|----------------------------------------|
|172.17.0.5|KDC|
|172.17.0.6|Hadoop NameNode Hadoop SecondaryNameNode|
|172.17.0.7|Hadoop DataNode |
|172.17.0.8|Hadoop DataNode |
|172.17.0.9|Hadoop DataNode |



### 创建用户组与用户

```shell
groupadd hadoop
useradd -s /bin/bash -g hadoop hdfs
useradd -s /bin/bash -g hadoop yarn
useradd -s /bin/bash -g hadoop mapred
```




### 服務竊用對應用戶
|ServerName       |用戶 |
|-----------------|----|
|NameNode.        |hdfs|
|SecondaryNameNode|hdfs|
|DataNode.        |hdfs|
|ResourceManager  |yarn|
|NodeManager      |yarn|





## Kerberos安装与配置
### 安装Kerberos

安装Krb5

```shell
yum install krb5-server krb5-libs krb5-auth-dialog
```

### 配置KDC

#### 修改/etc/krb5.conf
vim /etc/krb5.conf
修改realms和domain_realm节点
vim /var/kerberos/krb5kdc/kdc.conf
vim /var/kerberos/krb5kdc/kadm5.acl

#### 创建Database
备注：
> 该命令执行过程较长，需要等待
> 
> 如果需要重新聲稱文件，需要刪除/var/kerberos/krb5kdc/目錄中的principal前綴文件

```shell
/usr/sbin/kdb5_util create -s
```


#### 启动KDC

```shell
/etc/rc.d/init.d/krb5kdc start
/etc/rc.d/init.d/kadmin start
```

#### 创建Principals和Keytab文件

主要流程 

1.KDC服务器上输入以下命令，进入kadmin交互环境 

```shell
/usr/sbin/kadmin.local
```

2.使用addprinc新建Principals

```shell
addprinc -randkey $primary_name/$fully.qualified.domain.name@EXAMPLE.COM
```

>其中的$primary_name需要根据不同的服务角色进行修改
>
>$fully.qualified.domain.name 需要使用全路径的域名，例如node1.example.com
>
>规则参考http://hadoop.apache.org/docs/r3.0.2/hadoop-project-dist/hadoop-common/SecureMode.html#Kerberos_principals_for_Hadoop_Daemons

3.使用xst生成keytab文件

```shell
xst -norandkey -k $keytab_file_name $primary_name/fully.qualified.domain.name@EXAMPLE.COM
```


>$keytab_file_name 需要根据服务角色修改为不同的值

>4.传送keytab文件到各节点并放置到安全目录并设置权限


### 安装配置client

#### 修改HOST

在所有的节点/etc/hosts增加记录

```shell
172.17.0.5 kerberos.example.com
```

#### 安装包

```shell
yum install krb5-workstation
```

#### 配置krb5.conf

同步Kdc上的/etc/krb5.conf到所有的机器上


### HadoopNameNode配置

KDC服务器上 /usr/sbin/kadmin.local

```shell
addprinc -randkey HTTP/node1.example.com@EXAMPLE.COM
xst -norandkey -k spnego.service.keytab  HTTP/node1.example.com@EXAMPLE.COM
```

通过scp复制keytab文件后，执行如下命令

```shell
mkdir -p /etc/security/keytabs/
chown hdfs:hadoop /etc/security/keytabs
chmod 750 /etc/security/keytabs
cp /tmp/spnego.service.keytab /etc/security/keytabs/
chown hdfs:hadoop /etc/security/keytabs/spnego.service.keytab
chmod 400 /etc/security/keytabs/spnego.service.keytab
```

### 浏览器客户端配置
KDC服务器上 /usr/sbin/kadmin.local，创建新的principal并且修改密码

```shell
addprinc -randkey testuser1@EXAMPLE.COM
change_password testuser1@EXAMPLE.COM
```

客户度调用kinit登录并输入密码

```shell
kinit testuser1@EXAMPLE.COM
```

配置浏览器

参考地址
http://www.microhowto.info/howto/configure_firefox_to_authenticate_using_spnego_and_kerberos.html


### 检查
```shell
klist -e -k -t /etc/security/keytabs/spnego.service.keytab
```

## 配置HADOOP
### 配置环境变量
所有的环境配置

```shell
export HDFS_NAMENODE_USER="hdfs"
export HDFS_DATANODE_USER="hdfs"
export HDFS_SECONDARYNAMENODE_USER="hdfs"
export YARN_RESOURCEMANAGER_USER="yarn"
export YARN_NODEMANAGER_USER="yarn"

export HADOOP_CONF_DIR=/usr/local/hadoop/etc/hadoop
export JAVA_HOME=/usr/java/jdk1.8.0_45
export HBASE_HOME=/usr/local/hbase/
export HADOOP_HOME=/usr/local/hadoop
export HIVE_HOME=/usr/local/hive
export SPARK_HOME=/usr/local/spark-2.2.1-bin-without-hadoop
export PATH=$PATH:$JAVA_HOME/bin
export PATH=$PATH:$HBASE_HOME/bin
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
export PATH=$PATH:$HIVE_HOME/bin
```

### Hadoop NameNode

配置core-site.xml

```html
<property>
	<name>hadoop.http.filter.initializers</name>
	<value>org.apache.hadoop.security.AuthenticationFilterInitializer</value>
</property>
<property>
	<name>hadoop.http.authentication.type</name>
	<value>kerberos</value>
</property>
<property>
	<name>hadoop.http.authentication.kerberos.principal</name>
	<value>HTTP/node1.example.com@EXAMPLE.COM</value>
</property>
<property>
	<name>hadoop.http.authentication.kerberos.keytab</name>
	<value>/etc/security/keytabs/spnego.service.keytab</value>
</property>
```



[//]: #http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html

## 引用：

<a href="https://ambari.apache.org/1.2.5/installing-hadoop-using-ambari/content/ambari-kerb-1-4.html">1. https://ambari.apache.org/1.2.5/installing-hadoop-using-ambari/content/ambari-kerb-1-4.html</a>
<br/>
<a href="http://hadoop.apache.org/docs/r3.0.2/hadoop-project-dist/hadoop-common/SecureMode.html#Kerberos_principals_for_Hadoop_Daemons">2. http://hadoop.apache.org/docs/r3.0.2/hadoop-project-dist/hadoop-common/SecureMode.html#Kerberos_principals_for_Hadoop_Daemons</a>

