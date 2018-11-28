---
layout: post
title:  "Hbase集群添加删除RegionServer"
date:   2018-11-28 15:45:00 +0800
categories: Bigdata
---

### 添加RegionServer

master节点上执行

```shell
vim $HBASE_HOME/conf/regionservers
```

新regionserver上执行

```shell
hbase-daemons.sh start regionserver
```

### 删除RegionServer

regionserver上执行

```shell
hbase-daemons.sh start regionserver
```

master节点上执行

```shell
vim $HBASE_HOME/conf/regionservers
```

### 注意
在删除regionserver时候禁用 Load Balancer，使用如下命令

```shell
$HBASE_HOME/bin/graceful_stop.sh HOSTNAME
```

