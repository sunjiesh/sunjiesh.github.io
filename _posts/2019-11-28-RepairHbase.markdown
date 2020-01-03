---

layout: post 
title: "Hbase修复" 
date: 2019-11-28 00:00:00 +0800
categories: BigData
---

### Hbase region 某个regionserver挂掉后的处理
现象描述：某个regionserver服务挂掉后，此节点的Regions为0.  重启及数据恢复过程如下：（）
切记在hadoop用户下：



第一步：启动regionserver
/hbaseStallDir/bin/graceful_stop.sh 192.168.5.164
/hbaseStallDir/bin/hbase-daemon.sh start regionserver
/app/cloud/hadoop/bin/hadoop-daemon.sh start datanode


第二步：启动balancer
2）开启/关闭region
语法：balance_switch true|false
hbase(main)> balance_switch true
hbase(main)> balancer       （这步将导致hbase负载很大，因为各个节点不断的在同步数据，大量的io操作）

第三步：如果某些region卡住了，可根据 http://???.???.???.???:60010/master-status      Regions in Transition 的提示   用如下命令手工恢复region
/hbaseStallDir/bin/hbase hbck -repair Doc




### 引用 
[https://www.cnblogs.com/i80386/p/4127031.html](https://www.cnblogs.com/i80386/p/4127031.html).

