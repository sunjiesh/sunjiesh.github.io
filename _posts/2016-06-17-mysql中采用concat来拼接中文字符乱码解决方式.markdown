---
layout: post
title:  "mysql中采用concat来拼接中文字符乱码解决方式"
date:   2016-06-17 14:00:00 +0800
categories: Linux
---

mysql concat乱码问题解决 concat(str1,str2) 当concat结果集出现乱码时，大都是由于连接的字段类型不同导致，如concat中的字段参数一个是varchar类型，一个是int类型或 doule类型，就会出现乱码。
<br/> 
解决方法：利用mysql的字符串转换函数CONVERT将参数格式化为char类型就可以了。
<br/> 
举例： concat('数量:',CONVERT(int1,char),CONVERT(int2,char),'金 额:',CONVERT(double1,char),CONVERT(double2,char))