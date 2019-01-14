---

layout: post 
title: "订阅mosquitto服务器状态各主题" 
date: 2019-01-14 17:30:00 +0800
categories: Linux
---

## 订阅mosquitto服务器状态各主题

mosquitto_sub -v -t \$SYS/broker/client

MQTT客户端可以通过订阅位于$SYS层次下的主题来查看mosquitto服务器的状态信息。标记为Static的主题对于每一次订阅只发布一次。其它所有主题每隔sys_interval（在mosquitto.conf文件中配置）秒更新发布。如果sys_interval设置为０,系统就不发布更新。

$SYS中各主题说明如下：

$SYS/broker/bytes/received

自服务器启动以来共接收的字节数

$SYS/broker/bytes/sent

自服务器启动以来共发送的字节数

$SYS/broker/clients/connected, 

$SYS/broker/clients/active (1.4版本已取消)

当前连接的客户端数量

$SYS/broker/clients/expired

超过有效期被断开连接的客户端数量，有效期通过persistent_client_expiration参数设置。

$SYS/broker/clients/disconnected, 

$SYS/broker/clients/inactive (1.4版本已取消)

注册到服务器上的持久连接（clean seesion为假)但当前断开的客户端数量

$SYS/broker/clients/maximum

服务器同一时间连接的最大客户端数量

$SYS/broker/clients/total

有效和无效连接、注册到服务器上的总数。

$SYS/broker/connection/#

如果服务器设置了桥接，系统会提供一个主题来标识连接状态，默认使用$SYS/broker/connection/，如果主题值为１表示连接激活，如果为０表示连接没有激活。

$SYS/broker/heap/current size

Mosquitto正在使用的堆内存大小。注意这个主题是否可以使用取决于系统编译时的相关参数设置。

$SYS/broker/heap/maximum size

Mosquitto使用的最大堆内存。这个参数是否有效也取决于系统编译时的相关参数设置。

$SYS/broker/load/connections/+

不同时间段内服务器接收到的connections包的平均数。最后的“+”可是１min,5min,15min。分别表示１分钟，５分钟，15分钟的平均数。

$SYS/broker/load/bytes/received/+

不同时间段内服务器接收数据的平均字节数。最后的“+”可是１min,5min,15min。

$SYS/broker/load/bytes/sent/+

不同时间段内服务器发送数据的平均字节数。最后的“+”可是１min,5min,15min。

$SYS/broker/load/messages/received/+

不同时间段内服务器接收到的所有类型消息的平均数。最后的“+”可是１min,5min,15min。

$SYS/broker/load/messages/sent/+

不同时间段内服务器发送的所有类型的消息的平均数。最后的“+”可是１min,5min,15min。

$SYS/broker/load/publish/dropped/+

不同时间段内服务器丢弃的消息的平均数，这表明了那些持久连接但与服务器断开的客户端失去消息的速率。最后的“+”可是１min,5min,15min。

$SYS/broker/load/publish/received/+

不同时间段内服务器接收的发布消息的平均数。最后的“+”可是１min,5min,15min。

$SYS/broker/load/publish/sent/+

不同时间段内服务器发送的发布消息的平均数。最后的“+”可是１min,5min,15min。

$SYS/broker/load/sockets/+

不同时间段内服务器打开的socket连接的平均数。最后的“+”可是１min,5min,15min。

$SYS/broker/messages/inflight

等待确认的Qos>0的消息的数量。

$SYS/broker/messages/received

自服务器启动以来接收的所有类型的消息总数。

$SYS/broker/messages/sent

自服务器启动以来发送的所有类型的消息总数。

$SYS/broker/messages/stored

服务器存储的消息的总数，包括保留消息和持久连接客户端的消息队列中的消息数。

$SYS/broker/publish/messages/dropped

由于inflight/queuing限制而直接丢弃的消息的总数，相关设置请查看mosquitto.conf中max_inflight_messages 和max_queued_messages参数。

$SYS/broker/publish/messages/received

自服务器启动以来接收的发布消息的总数。

$SYS/broker/publish/messages/sent

自服务器启动以来发送的发布消息的总数。

$SYS/broker/retained messages/count

服务器保留的消息总数。

$SYS/broker/subscriptions/count

服务器订阅主题总数。

$SYS/broker/timestamp

Mosquitto软件build的详细时间（Static）。

$SYS/broker/uptime

Mosquitto启动时长（单位：秒）。

$SYS/broker/version

Mosquitto软件版本号（Static）。