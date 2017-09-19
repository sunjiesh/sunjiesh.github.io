---
layout: post
title:  "Load error: xxxx.so: cannot open shared object file: No such file or directory"
date:   2017-09-18 17:00:00 +0800
categories: Linux
---

碰到错误
<pre>
1505722995: Error: Unable to load auth plugin "/etc/mosquitto/auth-plug.so".
1505722995: Load error: libhiredis.so.0.13: cannot open shared object file: No such file or directory
</pre>
解决
<pre>
# cat /etc/ld.so.conf
include ld.so.conf.d/*.conf
# echo "/usr/local/lib" >> /etc/ld.so.conf
# ldconfig
</pre>
