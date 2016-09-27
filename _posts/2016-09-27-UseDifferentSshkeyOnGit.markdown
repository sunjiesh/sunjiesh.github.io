---
layout: post
title:  "Git配置多个Sshkey"
date:   2016-09-27 10:00:00 +0800
categories: Linux
---

在~/.ssh/config配置示例
<pre>
# github
Host github.com
HostName github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa
</pre>
