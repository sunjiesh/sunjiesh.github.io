---

layout: post 
title: "获取IP归属地方案" 
date: 2019-08-14 00:00:00 +0800
categories: Other
---

## taobao.com
### 访问限制
为了保障服务正常运行，每个用户的访问频率需小于1qps。
### 命令
```shell
http://ip.taobao.com/service/getIpInfo.php?ip=XX.XX.XX.XX
```

###返回

```
{"code":0,"data":{"ip":"XX.XX.XX.XX","country":"中国","area":"","region":"江苏","city":"无锡","county":"XX","isp":"电信","country_id":"CN","area_id":"","region_id":"320000","city_id":"320200","county_id":"xx","isp_id":"100017"}}
```

