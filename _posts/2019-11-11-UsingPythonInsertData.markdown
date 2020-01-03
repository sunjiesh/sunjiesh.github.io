---

layout: post 
title: "使用Python插入数据" 
date: 2019-10-11 10:00:00 +0800
categories: Python
---


## 准备工作

### 插入数据
```sql
CREATE TABLE `test`.`test_user` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(45) NOT NULL,
  `mobile` VARCHAR(45) NOT NULL,
  `create_time` DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `update_time` DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  PRIMARY KEY (`id`));
```

###脚本执行
```shell

# -*- coding: UTF-8 -*-

import datetime
import mysql.connector

mysql_host='localhost'
mysql_username='root'
mysql_password='password'

start_time = datetime.datetime.now()
db = mysql.connector.connect(host = mysql_host, user = mysql_username, passwd = mysql_password, database="test")
cursor = db.cursor()
start_mobile=13000000000
for index in range(100):
    try:
        mobile = start_mobile + index
        sql = "INSERT INTO `test`.`test_user`(`name`,`mobile`)VALUES('testuser{}','{}')".format(mobile,mobile)
        print sql
        cursor.execute(sql)
        db.commit()
    except Exception as e:
        print e
    
db.close()
end_time = datetime.datetime.now()
cost_time=end_time-start_time
print 'Insert finish,costtime is {}'.format(cost_time)


```