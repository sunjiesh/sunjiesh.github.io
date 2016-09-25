---
layout: post
title:  "Rsync安装与配置"
date:   2016-09-24 20:41:00 +0800
categories: Linux
---

服务器IP
Master:10.1.101.79
Slave:10.1.101.77


服务器之间作免登录配置，使用ssh-keygen

服务器端（Master端）
创建rsyncd.conf，这是rsync服务器的配置文件。
touch /etc/rsyncd.conf
创建rsyncd.secrets ，这是用户密码文件。
touch /etc/rsyncd.secrets  
将rsyncd.secrets这个密码文件的文件属性设为root拥有, 且权限要设为600, 否则无法备份成功!
chmod 600 /etc/rsyncd.secrets
touch /etc/rsyncd.motd

修改配置

修改权限
chown root:root /etc/rsyncd.secrets
chmod 600 /etc/rsyncd.secrets

在备机上创建对应的文件，该文件与主机上的rsyncd.secrets对应
vi /etc/rsyncd.password
chmod 600 /etc/rsyncd.password

启动
/usr/bin/rsync --daemon


客户端，做与主机相同操作


测试-主机文件到备机：
Master上执行
echo "bbbbbb">>test.txt
Slave执行
/usr/bin/rsync -vzrtopg --progress --delete 10.1.101.79::sharefile /home/sharefile --password-file=/etc/rsyncd.password


测试-备机文件到主机：
Slave执行
echo "bbbbbb">>test5555.txt
Master上执行
/usr/bin/rsync -vzrtopg --progress --delete 10.1.101.77::sharefile /home/sharefile  --password-file=/etc/rsyncd.password


备机执行定时任务
crontab -e
*/2 * * * * /usr/bin/rsync -vzrtopg --progress --delete 10.1.101.79::sharefile /home/sharefile --password-file=/etc/rsyncd.password


主机 vi /etc/rc.d/rc.local
rsync --daemon
nohup /usr/bin/rsync -vzrtopg --progress --delete 10.1.101.77::sharefile /home/sharefile --password-file=/etc/rsyncd.password &
