---
layout: post
title:  "attempt to call ngx.exec after sending out response headers解决"
date:   2016-04-15 11:16:00 +0800
categories: Nginx
---

去除Lua中的ngx.say等输出语句

已经输出了响应头的情况下再用 ngx.exec() 发起内部跳转是无意义的，因为跳转到的目标 location输出它自己的响应头就会导致非法 HTTP 响应了。


参考：<a href="https://groups.google.com/forum/#!msg/openresty/z83AeHX1XDQ/yRNiD4Ng-rkJ" target="_blank">https://groups.google.com/forum/#!msg/openresty/z83AeHX1XDQ/yRNiD4Ng-rkJ</a>
