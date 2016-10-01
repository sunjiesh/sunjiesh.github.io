---
layout: post
title:  "调整linux系统时间和时区与Internet时间同步"
date:   2016-10-01 10:07:20 +0800
categories: Linux
---

## 简要分为以下3个步骤：
### 一、修改时区
<pre><code>
cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
</pre></code>
修改为中国的东八区
<pre><code>
vi /etc/sysconfig/clock
ZONE="Asia/Shanghai"
UTC=false
ARC=false
</pre></code>


### 二、配置新的时间
日期设定：
<pre><code>
# date -s 2013/09/26
</pre></code>

时间设定：
<pre><code>
# date -s 11:47:06
# date -s "12:00:00 2013-12-06"
# date -s "12:00:00 20131206"
# date -s "2013-12-06 12:00:00"
# date -s "20131206 12:00:00"
</pre></code>

date是显示的系统OS时间
clock是显示Bios的时间
查看硬件时间（BIOS的）：
 hwclock [-rw] 
 -r:查看现有BIOS时间，默认为－r参数
 -w:将现在的linux系统时间写入BIOS中
-s(systohc):将硬件时间调整为和目前的系统时间一样
#hwclock -s : 
#hwclock -w : 将linux内部时间写入更新到bios/cmos内
 当我们进行完 Linux 时间的校时后，还需要以 hwclock -w 来更新 BIOS 的时间，因为每次开机的时候，系统会重新由 BIOS 将时间读出来，所以， BIOS 才是重要的时间依据。
# hwclock
2013年09月26日 星期四 11时49分10秒 -1.002805 seconds
修改系统时间（date）后，要同步BIOS时钟，强制把系统时间写入CMOS：
# clock -w或者# hwclock -w

### 三、实现Internet时间同步（这里可以忽略上面两步）
方法1. 开机的时候自动网络校时： 
 vi /etc/rc.d/rc.local 
 /usr/sbin/ntpdate -u 192.168.0.2 192.168.0.3 192.168.0.4;  /sbin/hwclock -w
后面的ip对应的是局域网内需要时间相同同步的主机。

方法2. 设定计划任务 
crontab格式如下：
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

# For details see man 4 crontabs

# Example of job definition:
# .---------------- minute (0 - 59)
# | .------------- hour (0 - 23)
# | | .---------- day of month (1 - 31)
# | | | .------- month (1 - 12) OR jan,feb,mar,apr ...
# | | | | .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# | | | | |
# * * * * * user-name command to be executed

设定crontab计划任务也有两种方式：
1、写在/etc/crontab里
代码:
0 12 * * * root ntpdate 210.72.145.44
每天11点与中国国家授时中心同步时间
当然前提是
#yum -y install ntpdate
代码也可是
0 12 * * * root ntpdate asia.pool.ntp.org
2、使用命令crontab -e
crontab -e 
 0 12 * * * root ntpdate asia.pool.ntp.org;hwclock -w

手动和时间服务器校准时间：
1.首先关闭ntpd服务：
#service ntpd stop 
2.然后和时间服务器校准：
#ntpdate asia.pool.ntp.org
3.同步BIOS时间：
#hwclock -w
4.校准后然后开启ntpd服务
#service ntpd start

来源： <http://liumissyou.blog.51cto.com/4828343/1302050>
 
