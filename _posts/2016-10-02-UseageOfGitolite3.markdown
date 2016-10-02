---
layout: post
title:  "Gitolite3 使用"
date:   2016-10-02 09:28:20 +0800
categories: Linux
---
### 主要通过如下几步
#### 通过ssh-keygen生成密钥
<pre>
ssh-keygen
cp .ssh/rd_rsa.pub /tmp
</pre>

#### 新建Git用户
<pre>
useradd git
</pre>

#### 安装Gitolite3
<pre>
apt-get install gitolite3
</pre>
#### 使用Git用户权限操作
<pre>
su - git
gitolite setup --pubkey /tmp/id_rsa.pub
</pre>
