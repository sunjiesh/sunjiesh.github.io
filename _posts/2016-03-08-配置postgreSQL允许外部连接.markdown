---
layout: post
title:  "配置postgreSQL允许外部连接"
date:   2016-03-08 19:00:03 +0800
categories: postgresql
---

 postgreSQL默认不允许外部连接，需要进行配置才行，postgreSQL版本是8.4.4。进入%postgreSQL_path%\8\data目录，打开pg_hba.conf文件，找到下面这段：
# TYPE DATABASE    USER        CIDR-ADDRESS          METHOD

# IPv4 local connections:
host    all         all         127.0.0.1/32          md5
# IPv6 local connections:
#host    all         all         ::1/128                 md5

在# IPv4 下一系列的host增加一行：
host    all         all         192.168.80.1/24        md5
这行的意思是允许所有 192.168.80.*** 这样ip访问本机postgreSQL服务。这里要说明一下，原有的
host    all         all         127.0.0.1/32          md5
这一行不要删除， 我第一次配置时就因为直接修改这行，然后导致postgreSQL服务无法启动。而postgreSQL启动失败后，有很多postgres的进程无法自 动关闭，使用任务管理器是无法手动把它们全部关闭的，因为postgreSQL会自动开启新的进程，经常你关了一个，它又打开了很多个。最后我是借用 cports工具的“终止打开选中窗口的进程”功能，才把postgreSQL全部给关闭的。

      postgreSQL服务无法启动，也有说解决方法如下：
修改本地链接属性：
本地链接->属性->Internet协议（TCP/IP）->属性->常规 ->高级->WINS->启动 LMHOSTS查询
已选上则点去前面的钩（如果没有则勾上）。确定，确定，关闭。
然后你就会发现postgres服务可以启动了。

原因是Dr.com的工作方式修改了Winsock LSP，致使postgres服务无法正常启动。

postgres服务启动后一直会开在那里，期间可以正常使用Dr.com（弹出对话框不要选择重启），但是启动重启之后PostgreSQL又不能使用了。

遇到这种情况请重复以上步骤，勾上或者去掉“启动 LMHOSTS查询”前的钩，改变状态就行。
然后就又可以了。
      我遇到的问题不属于这种情况，经测试无效。

同时修改postgresql.conf文件，
listen_addresses = '*'
我本机中默认就是如上配置，也就是我在安装的时候就设置了允许所有地址。

配置说明：
# TYPE DATABASE USER CIDR-ADDRESS METHOD
说明每一行有五个字段，
分别是：连接类型、可使用的数据库名、使用者、DIDR地址、和验证方法等五项。
下面，我只介绍一些针对每个字段常用的选项。

字段一：TYPE。
可以选择：local或host。
前者只能允许本地的用户登陆Postgres数据库;后者可以接受远程客户登陆。所以，
我们应该使用“host”。

字段二：DATWABSE。
连接用户可以使用的数据库名字。可以使Postgres的一个具体的
数据库名，也可以使用“all”来允许用户访问所有数据库。

字段三：USER。可以指定某个具体的用户来连接Postgres数据库(还要结合后面的地址字段)，
也可以使用“all”来允许所有用户连接数据库。

字段四：DIDR-ADDRESS。
是IP地址与掩码的另一种表示方法。
Postgres是通过这个字段来了解，允许那些IP或IP网段连接此服务器。
它的格式是： IP地址/掩码。
这个掩码和子网掩码是一个道理，只不过是用一个小于等于32的正数来表示，
表示的正是子网掩码中高几位为1，
比如，255.255.255.0 就是“24”，说明高24位是1。
192.168.0.1/32 相当于 IP为192.168.0.1，子网掩码为255.255.255.255的网段，
很显然，这只表明192.168.0.1IP自己。

字段五：METHOD。
这是验证方法。可选的有：
reject：拒绝这个IP的用户访问;
md5：密码以md5作为hash编码;
password：密码作为明文传输(好恐怖!);
krb5：密码以krb5作为hash编码。

下面举一个例子，来说明如何进行设置：
# TYPE DATABASE USER CIDR-ADDRESS METHOD
#允许IP为192.168.0.1的所有用户登陆到Postgres服务器的所有数据库，采用md5验证。
host all all 192.168.0.1/32 md5
#允许用户testuser在192.168.0.XX的网段任意机器登陆Postgres服务器，
#只能使用数据库testdb，采用md5验证。
host testdb testuser 192.168.0.1/24 md5

2. 改监听地址
默认下，POSTGRESQL只接受本地服务，要接受远程服务，需改postgresql.conf 文件listen_address = *

3. 如果是在Linux上的PostgreSQL
要打开 “unix的tcpip套接子”。
编辑 $POSTGRES/data/postgresql.conf 文件，
将tcpip_socket=off改成tcpip_socket=on即可。

配置说明部分摘自文章：http://hi.baidu.com/593313600/blog/item/12f2a8d17ccef4db572c8442.html
