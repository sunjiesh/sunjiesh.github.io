---

layout: post 
title: "
Restart SSH/sshd in Mac OS X" 
date: 2019-05-24 10:00:00 +0800
categories: Linux
---



# Restart SSH/sshd in Mac OS X

```shell
sudo launchctl stop com.openssh.sshd
sudo launchctl start com.openssh.sshd

```


引用 [http://vivo.pub/2409](http://vivo.pub/2409).