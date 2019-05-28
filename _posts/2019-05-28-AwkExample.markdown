---

layout: post 
title: "Awk Example" 
date: 2019-05-28 00:00:00 +0800
categories: Linux
---



# Awk Example

```shell
awk -F ',' 'BEGIN{sum=0}{sum+=$2}END{print sum}'

```


引用 [https://www.chedong.com/blog/archives/000682.html](https://www.chedong.com/blog/archives/000682.html).