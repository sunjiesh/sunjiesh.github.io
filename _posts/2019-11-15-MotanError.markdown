---

layout: post 
title: "Motan常见错误" 
date: 2019-10-15 10:00:00 +0800
categories: Java
---


### request_counter=743 =993 max_thread=1000 这个错误是什么原因导致的？


这个错误是触发了线程保护策略。
在端口提供多个method时，motan提供了简单的线程保护策略防止单个方法请求将worker线程耗尽，如下场景会触发此异常（细节请参考ProviderProtectedMessageRouter类）：

如果接口有多个方法，那么如果单个method超过 maxThread / 2 && totalCount > (maxThread * 3 / 4);
如果接口有多个方法(4个)，同时总的请求数超过 maxThread * 3 / 4，同时该method的请求数超过 maxThead * 1 / 4

从异常信息看，server端配置了1000worker线程，目前使用的总线程数为993，被reject的方法占用743，满足上述第1个场景。
建议解决办法
1是想办法提高业务处理效率，减少单个请求的处理耗时；
2是增加server节点数量，降低单server的qps；
3是如果服务端性能良好可以增加处理线程数量，例如1500