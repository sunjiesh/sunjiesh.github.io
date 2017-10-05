---
layout: post
title:  "Maven Deploy file example"
date:   2017-10-05 22:00:00 +0800
categories: Maven
---

<pre><code>
mvn deploy:deploy-file -Durl=http://localdellserver:8081/repository/third/ -DrepositoryId=third -Dfile=alipay-sdk-java20170829142630.jar -DgroupId=com.alipay -DartifactId=alipay-sdk -Dversion=20170829142630 -Dsources=alipay-sdk-java20170829142630-source.jar
</code></pre>

<pre><code>
mvn deploy -DskipTests=true -DaltDeploymentRepository=maven-snapshots::default::http://localdellserver:8081/repository/maven-snapshots/
</code></pre>
