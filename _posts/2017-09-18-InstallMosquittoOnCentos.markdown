---
layout: post
title:  "Centos上源码安装mosquitto"
date:   2017-09-18 15:00:00 +0800
categories: Linux
---

依赖包安装:
<pre>
yum install gcc
yum install gcc-c++
yum install openssl-devel
yum install libuuid libuuid-devel
</pre>

主要安装步骤
1. make
2. make instlal

碰到的问题描述
./mosquitto_internal.h:40:20: error: ares.h: No such file or directory
<br/>
解决
<pre>
vi config.mk
WITH_SRV:=no  
</pre>

