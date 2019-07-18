---

layout: post 
title: "git仓库迁移和更新远程仓库地址" 
date: 2019-07-17 00:00:00 +0800
categories: Git
---

一、git仓库迁移

1，从原仓库clone或pull到本地仓库

git clone project_name ​【old_remote_repository_address】

2，​在新的git创建一个新仓库。如果用gitolite搭建的git服务器，那么只需要在配置文件gitolite.conf上添加仓库和用户，然后push到服务器即可。

3，进入clone下来的本地仓库目录，将远程仓库地址修改为新的远程仓库地址

project_name> git remote remove origin

 project_name> git remote add origin【new_remote_repository_address】

4，将本地仓库文件push到新的远程仓库

project_name> ​gitpush origin master

二、修改​远程仓库地址

两种方式，除了上面第3步的修改方法，还可以：

git remote set-url origin ​【new_remote_repository_address】


## 引用
[https://www.cnblogs.com/softidea/p/5827361.html](https://www.cnblogs.com/softidea/p/5827361.html).
