---
layout: post
title:  "centos selinux不重启关闭"
date:   2016-09-30 09:54:40 +0800
categories: Linux
---

### 关闭SELinux的方法：
修改/etc/selinux/config文件中的SELINUX="" 为 disabled ，然后重启。<br/>
如果不想重启系统，使用命令setenforce 0<br/>
注：<br/>
setenforce 1 设置SELinux 成为enforcing模式<br/>
setenforce 0 设置SELinux 成为permissive模式<br/>
在lilo或者grub的启动参数中增加：selinux=0,也可以关闭selinux<br/>

### 查看selinux状态：
/usr/bin/setstatus -v<br/>
如下：<br/>
SELinux status:                 enabled<br/>
SELinuxfs mount:                /selinux<br/>
Current mode:                   permissive<br/>
Mode from config file:          enforcing<br/>
Policy version:                 21<br/>
Policy from config file:        targeted<br/>

### getenforce/setenforce查看和设置SELinux的当前工作模式
发现服务一启动，马上停止，在网上查找资料，找到安装时要先禁用SELinux，再安装MySQL，步骤是：
1. 关闭SELinux，重启系统；
2. 安装MySQL（MySQL server应该可以启动了）；
3. 启用SELinux，重启系统，之后MySQL server就可以正常启动了。
 启用禁用SELinux的方法是：<br/>
 vi /etc/selinux/config（也有人说是/etc/sysconfig/selinux文件，其实两个之间是链接关系，随便改其中一个，另一个也改了）<br/>
 SELINUX=disable 禁用SeLinux<br/>
 SELINUX=enforcing 启用SeLinux<br/>



引用：http://www.2cto.com/os/201108/102001.html
