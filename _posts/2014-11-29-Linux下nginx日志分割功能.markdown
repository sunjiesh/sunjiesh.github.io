---
layout: post
title:  "Linux下nginx日志分割功能"
date:   2014-11-29 00:00:00 +0800
categories: linux
---

主要分为如下几个操作

创建管道
mkfifo /usr/local/nginx/logs/access_log_pipe

执行
nohup cat /usr/local/nginx/logs/access_log_pipe | cronolog /usr/local/nginx/logs/%Y%m%d/access_%Y%m%d%H.log &

修改nginx配置
access_log  /usr/local/nginx/logs/access_log_pipe;

nginx 配置重新加载
service nginx reload
