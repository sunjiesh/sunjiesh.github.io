---
layout: post
title:  "Java JDBC Thin Driver 连接 Oracle 三种方法说明"
date:   2017-09-15 10:00:00 +0800
categories: Oracle
---

## 格式一:  Oracle JDBC Thin using a ServiceName: 

jdbc:oracle:thin:@//<host>:<port>/<service_name> 
Example: jdbc:oracle:thin:@//192.168.2.1:1521/XE

注意这里的格式，@后面有//, 这是与使用SID的主要区别。
这种格式是Oracle 推荐的格式，因为对于集群来说，每个节点的SID 是不一样的，但是SERVICE_NAME 确可以包含所有节点。

 
## 格式二: Oracle JDBC Thin using an SID: 
jdbc:oracle:thin:@<host>:<port>:<SID> 
Example: jdbc:oracle:thin:192.168.2.1:1521:X01A 

Note: Support for SID is being phased out. Oracle recommends that users switch over to usingservice names.


 
## 格式三：Oracle JDBC Thin using a TNSName: 

jdbc:oracle:thin:@<TNSName> 
Example: jdbc:oracle:thin:@GL 

Note: 
Support for TNSNames was added in the driver release 10.2.0.1
