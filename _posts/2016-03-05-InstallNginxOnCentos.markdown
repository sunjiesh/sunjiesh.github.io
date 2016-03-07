---
layout: post
title:  "Install Nginx On Centos"
date:   2016-03-05 00:00:00 +0800
categories: linux
---

1、安裝類庫
yum -y install pcre-devel openssl openssl-devel

2、下載Nginx
wget http://nginx.org/download/nginx-1.5.2.tar.gz
3、解壓Nginx
tar zxvf nginx-1.5.2.tar.gz 

4、編譯安裝
   cd nginx-1.5.2
   ./congigure
  如果顯示如下，則表示系統符合安裝條件

<a href="http://114.215.198.198/wp-content/uploads/2016/03/05/nginx_configure.png"><img class="alignnone size-full wp-image-67" src="http://114.215.198.198/wp-content/uploads/2016/03/05/nginx_configure.png"  /></a>

make
make install

5、配置運行
cd /usr/local/nginx/
sbin/nginx

瀏覽器打開http://192.168.1.18/，顯示出如下界面表示安裝成功

<a href="http://114.215.198.198/wp-content/uploads/2016/03/05/nginx_index.png"><img class="alignnone size-full wp-image-67" src="http://114.215.198.198/wp-content/uploads/2016/03/05/nginx_index.png"   /></a>



如果打開不了，可能是由於防火牆的原因，需要關閉防火牆
/etc/init.d/iptables stop






