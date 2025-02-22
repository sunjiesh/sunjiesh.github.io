---

layout: post 
title: "Docker常用镜像" 
date: 2025-02-22 17:00:00 +0800
categories: Software
---


```shell
mkdir /data/nexus-data && chown -R 200 /data/nexus-data
docker run -d --name nexus3 -p 18081:8081 --restart always -v /data/nexus-data:/nexus-data sonatype/nexus3

```

```shell
docker run -d --name sonarqube -e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true -p 9000:9000 sonarqube:latest

```