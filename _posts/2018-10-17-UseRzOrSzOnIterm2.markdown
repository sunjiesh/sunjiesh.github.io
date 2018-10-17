---

layout: post 
title: "iTerm2使用rz、sz远程上传或下载文件" 
date: 2018-10-27 14:30:00 +0800
categories: Linux
---

# iTerm2使用rz、sz远程上传或下载文件

### 安装rzsz

```shell
brew install lrzsz
```

### 安装iterm2-zmodem


```shell
cd /usr/local/bin
sudo wget https://raw.github.com/mmastrac/iterm2-zmodem/master/iterm2-send-zmodem.sh
sudo wget https://raw.github.com/mmastrac/iterm2-zmodem/master/iterm2-recv-zmodem.sh
sudo chmod 777 /usr/local/bin/iterm2-*
```

打开Item2，点击preferences → profiles，选择某个profile，如Default，之后继续选择advanced → triggers，添加编辑添加如下triggers：

```shell
Regular expression: rz waiting to receive.\*\*B0100
Action: Run Silent Coprocess
Parameters: /usr/local/bin/iterm2-send-zmodem.sh
Instant: checked

Regular expression: \*\*B00000000000000
Action: Run Silent Coprocess
Parameters: /usr/local/bin/iterm2-recv-zmodem.sh
Instant: checked
```