---
layout: post
title:  "运用MQTT-JMeter插件测试MQTT服务器性能"
date:   2018-12-20 19:15:00 +0800
categories: Iot
---

```shell
export PATH=$PATH:<JDK_HOME>/bin

keytool -import -alias cacert -keystore emqtt.jks -file cacert.pem -storepass <Your_Secret> -trustcacerts -noprompt

keytool -import -alias client -keystore emqtt.jks -file client-cert.pem -storepass <Your_Secret>

keytool -import -alias server -keystore emqtt.jks -file cert.pem -storepass <Your_Secret>

openssl pkcs12 -export -inkey client-key.pem -in client-cert.pem -out client.p12 -password pass:<Your_Secret>
```


User authentication: 如果服务器配置了用户认证，您需要提供相应的用户名和口令。

ClientId prefix: 标识客户端的固定前缀，每个连接(虚拟用户)再添加一个uuid串，整个作为客户标识。

Keep alive(s): 心跳信号发送间隔。例如，300表示客户端每隔300秒向服务器发出ping请求，以保持连接活跃。

Connection keep time(s): 连接建立后，保持该连接的时长。例如，1800表示1800秒之后连接将被关闭，即使一直发送心跳信号。

Connect attempt max: 第一次连接过程中，尝试重连的最大次数。超过该次数则认为连接失败。

Reconnect attempt max: 后继连接过程中，尝试重连的最大次数。超过该次数则认为连接失败。
