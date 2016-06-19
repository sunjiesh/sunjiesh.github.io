---
layout: post
title:  "Tomcat+MongoDB Sesson共享"
date:   2016-06-19 15:20:00 +0800
categories: Mysql
---

Tomcat+MongoDB Sesson共享
<br/>
使用Mongo-Tomcat-Sessions，项目地址https://github.com/simplicityitself/Mongo-Tomcat-Sessions
<br/>
1、git下载并打包
<br/>
2、mongo-java-driver-2.4.jar和mongo-store-1.5.jar放入tomcat的lib下
<br/>
3、修改context.xml，加入
<br/>
<pre>
	<Valve className="com.dawsonsystems.session.MongoSessionTrackerValve" />
	<Manager className="com.dawsonsystems.session.MongoManager" host="localhost" port="27017" database="sessions" maxInactiveInterval="84"/>
</pre>
	
<br/>
4、启动tomcat测试
<br/>