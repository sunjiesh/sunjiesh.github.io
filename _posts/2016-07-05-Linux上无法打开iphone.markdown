---
layout: post
title:  "Linux上无法打开iphone"
date:   2016-07-05 15:41:00 +0800
categories: Linux
---
与正常的syslog进行对比，发现是少了gvfs，安装即可
<pre>
sudo apt-get install gvfs*
</pre>
<img src="http://114.215.198.198/wp-content/uploads/2016/07/05/Screenshot_2016-07-05_11-52-40.png"/>
