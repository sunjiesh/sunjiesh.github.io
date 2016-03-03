---
layout: post
title:  "bash:fork:Resource temporarily unavailable  "
date:   2015-01-30 07:39:00 +0800
categories: linux
---

通过调用ulimit -u 4096即可解决，否則只在當前shell下有效。

需要修改文件。

vi /etc/security/limits.conf
<wbr /> <wbr /> <wbr /> # 添加如下的行
<wbr /> <wbr /> <wbr /> * soft noproc 11000
<wbr /> <wbr /> <wbr /> * hard noproc 11000
<wbr /> <wbr /> <wbr /> * soft nofile 4100
<wbr /> <wbr /> <wbr /> * hard nofile 4100

<wbr /> <wbr /> <wbr /> 说明：* 代表针对所有用户
<wbr /> <wbr /> <wbr /> noproc 是代表最大进程数
<wbr /> <wbr /> <wbr /> nofile 是代表最大文件打开数

&nbsp;

引用:<a href="http://houjixin.blog.163.com/blog/static/3562841020138611573918/">http://houjixin.blog.163.com/blog/static/3562841020138611573918/</a>
