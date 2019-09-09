---
layout: post
title:  "Mysql 方法"
date:   2019-09-09 10:00:00 +0800
categories: Mysql
---

### MySql中String转int

```shell
SELECT CAST('123' AS SIGNED);
SELECT CONVERT('123',SIGNED);
SELECT '123'+0;
```

### 引用

[https://blog.csdn.net/er_shao_ye/article/details/50987994](https://blog.csdn.net/er_shao_ye/article/details/50987994)