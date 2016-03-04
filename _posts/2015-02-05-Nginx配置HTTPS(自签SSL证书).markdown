---
layout: post
title:  "Nginx配置HTTPS(自签SSL证书)"
date:   2015-02-05 08:37:03 +0800
categories: jekyll update
---

前置条件
nginx 编译安装需要设置--with-http_ssl_module参数
./configure --with-http_ssl_module

1.首先要生成服务器端的私钥(key文件):
openssl genrsa -des3 -out server.key 1024
运行时会提示输入密码,此密码用于加密key文件

<a href="http://www.sunjiesh.com.cn/wp-content/uploads/2015/01/001-生成ssl私钥.png"><img class="alignnone size-full wp-image-56" src="http://www.sunjiesh.com.cn/wp-content/uploads/2015/01/001-生成ssl私钥.png" alt="001-生成ssl私钥" width="1044" height="244" /></a>

去除key文件口令的命令:
openssl rsa -in server.key -out server.key

<a href="http://www.sunjiesh.com.cn/wp-content/uploads/2015/01/002-生成ssl私钥2.png"><img class="alignnone size-full wp-image-55" src="http://www.sunjiesh.com.cn/wp-content/uploads/2015/01/002-生成ssl私钥2.png" alt="002-生成ssl私钥2" width="718" height="96" /></a>

2. openssl req -new -key server.key -out server.csr
生成Certificate Signing Request（CSR）,生成的csr文件交给CA签名后形成服务端自己的证书.屏幕上将有提示,依照其指示一步一步输入要求的个人信息即可.

<a href="http://www.sunjiesh.com.cn/wp-content/uploads/2015/01/003-gen_csr_file.png"><img class="alignnone size-full wp-image-54" src="http://www.sunjiesh.com.cn/wp-content/uploads/2015/01/003-gen_csr_file.png" alt="003-gen_csr_file" width="842" height="156" /></a>

3.openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt

<a href="http://www.sunjiesh.com.cn/wp-content/uploads/2015/01/004-gen_crt_file.png"><img class="alignnone size-full wp-image-53" src="http://www.sunjiesh.com.cn/wp-content/uploads/2015/01/004-gen_crt_file.png" alt="004-gen_crt_file" width="914" height="36" /></a>

4.nginx 配置增加

listen 443;
ssl on;
ssl_certificate /usr/local/nginx/conf/server.crt;
ssl_certificate_key /usr/local/nginx/conf/server.key;

&nbsp;

<a href="http://www.sunjiesh.com.cn/wp-content/uploads/2015/01/005-nginxpezhi.png"><img class="alignnone size-full wp-image-52" src="http://www.sunjiesh.com.cn/wp-content/uploads/2015/01/005-nginxpezhi.png" alt="005-nginxpezhi" width="705" height="190" /></a>

5.service nginx start

在浏览器打开http://officecentosvm001/和https://officecentosvm001/ 都能出现为Nginx欢迎页面,表示配置成功
