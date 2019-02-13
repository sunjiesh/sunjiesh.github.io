---

layout: post 
title: "Java读取文件MD5" 
date: 2019-02-23 14:00:00 +0800
categories: Java
---

```java

FileInputStream fis= new FileInputStream(path);  
String md5 = DigestUtils.md5Hex(IOUtils.toByteArray(fis));  
IOUtils.closeQuietly(fis);  
System.out.println("MD5:"+md5); 

```

参考<br/>
[https://blog.csdn.net/wangqiuyun/article/details/22941433](https://blog.csdn.net/wangqiuyun/article/details/22941433 )