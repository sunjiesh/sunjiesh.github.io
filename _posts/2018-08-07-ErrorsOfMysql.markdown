---

layout: post 
title: "Mysql 常见错误" 
date: 2018-08-07 17:30:00 +0800
categories: Mysql
---

## Error Code: 1175. You are using safe update mode and you tried to update a table without a WHERE that uses a KEY column To disable safe mode, toggle the option in Preferences -> SQL Editor and reconnect.

```shell
SET SQL_SAFE_UPDATES = 0;

```
