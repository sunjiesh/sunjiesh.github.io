---
layout: post
title:  "清理MySQL的log-bin日志"
date:   2016-06-18 10:15:00 +0800
categories: Mysql
---

<pre>
如果只有一台MySQL服务器则登录MySQL后：
#删除某个日志之前的日志
PURGE BINARY LOGS TO 'mysql-bin.110';
#或删除某个时间点以前的日志
PURGE BINARY LOGS BEFORE '2011-05-05 00:30:00';
如果是主从数据库，则登录MySQL后：
#在所有从库上检查它正在读取哪个日志，执行
SHOW SLAVE STATUS;
#清理日志
PURGE MASTER LOGS BEFORE '2011-05-05 00:30:00';
#然后在主服务器上执行
PURGE BINARY LOGS BEFORE '2011-05-05 00:30:00';
自动清理:
#配置my.cnf
#增加expire_logs_days = 天数
#例如保留5天
expire_logs_days = 5

</pre>