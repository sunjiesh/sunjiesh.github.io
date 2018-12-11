---
layout: post
title:  "hadoop 查看集群的网页监控状态"
date:   2018-12-11 11:36:00 +0800
categories: BigData
---
一、查看集群的网页监控状态

1.查看hdfs集群状态，也就是namenode的访问地址

配置：hdfs-site.xml--dfs.namenode.http-address

默认访问地址：http://namenode的ip:50070

2.如果配置了secondary namenode，那么可以查看secondary namenode的集群状态

配置：hdfs-site.xml--dfs.namenode.secondary.http-address

默认访问地址：http://namenode的ip:50090

3.查看yarn集群的状态

配置：yarn-site.xml--yarn.resourcemanager.webapp.address

默认访问地址：http://resource manager的ip:8088 

