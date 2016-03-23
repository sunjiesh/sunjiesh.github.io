---
layout: post
title:  "Virtualbox重新配置dkms并加载vboxdrv模块"
date:   2016-03-23 10:19:03 +0800
categories: virtualbox
---

sudo dpkg-reconfigure virtualbox-dkms

sudo modprobe vboxdrv


参考：
<a target="_blank" href="http://www.linuxdashen.com/%E8%A7%A3%E5%86%B3virtualbox-kernel-driver-not-installed%E9%94%99%E8%AF%AF">http://www.linuxdashen.com/%E8%A7%A3%E5%86%B3virtualbox-kernel-driver-not-installed%E9%94%99%E8%AF%AF</a>
