---

layout: post 
title: "iTerm2配置clone session功能" 
date: 2019-12-27 00:00:00 +0800
categories: Linux
---

### iTerm2打开reuse

顶部导航栏Profiles -> 配置在使用的Profiles -> General -> Working Directory -> 选中“Reuse previous session’s directory”

### 配置Mac所在机器ssh

```
vim ~/.ssh/config

host * 
ControlMaster auto 
ControlPath ~/.ssh/master-%r@%h:%p
```

### 确认是否生效

重新ssh relay机器，并判断~/.ssh/目录下是否生成master-*的sock文件。
这样，继续登录相同机器，就复用上述链接。

### clone session alias

配个alias，在本机已经登录同一服务器的情况下，简单一句话ssh就OK了

```
#alias ssh relay
alias relay=’sh ~/bin/relay/ssh_to_relay.sh’
```

```
ssh_to_relay.sh

    ssh relay01.google.com
```