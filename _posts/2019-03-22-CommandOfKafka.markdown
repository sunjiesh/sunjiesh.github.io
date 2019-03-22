---

layout: post 
title: "Kafka命令" 
date: 2019-03-22 10:00:00 +0800
categories: Java
---

## 常用命令

### start zookeeper and kafka

```shell
bin/zookeeper-server-start.sh config/zookeeper.properties
bin/kafka-server-start.sh config/server.properties
```

### Create a topic

```shell
bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
bin/kafka-topics.sh --list --zookeeper localhost:2181
```

### Send some messages
```shell
bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test
```

### Start a consumer
```shell
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning
```