---

layout: post 
title: "java实现监听mqtt客户端是否在线" 
date: 2020-01-20 09:32:00 +0800
categories: Java
---

"$SYS/brokers/+/clients/+/connected";//客户端上线主题 所有节点的 所有设备

"$SYS/brokers/+/clients/+/disconnected";//客户端下线主题

订阅以上两个主题即可

