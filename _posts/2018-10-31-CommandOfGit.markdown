---
layout: post
title:  "Git常用命令总结"
date:   2018-10-30 11:00:00 +0800
categories: Git
---

### Git clone

```shell
git clone git@github.com:sunjiesh/xxx.git
```

### git cherry-pick

```shell
git cherry-pick <commit id>
```

### git 放弃本地修改 强制更新
```shell
git fetch --all
git reset --hard origin/master
```
git fetch 只是下载远程的库的内容，不做任何的合并 git reset 把HEAD指向刚刚下载的最新的版本


