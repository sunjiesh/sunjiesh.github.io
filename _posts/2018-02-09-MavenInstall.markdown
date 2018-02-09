---
layout: post
title:  "Maven  install file example"
date:   2018-02-09 10:00:00 +0800
categories: Maven
---

<pre><code>
mvn install:install-file -Dfile=D:\xmlunit-1.3.jar -DgroupId=org.custommonkey -DartifactId=xmlunit -Dversion=1.3 -Dpackaging=jar -DgeneratePom=true
-DcreateChecksum=true
</code></pre>

