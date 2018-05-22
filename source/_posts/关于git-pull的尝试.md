---
title: 关于git pull的尝试
date: 2018-05-17 15:34:58
tags:      
- git pull
category: git
---
# 1.文件版本不一致，导致冲突
本地文件host.conf，修改当前版本v1：env：preview，  
线上host.conf，刚提交一个版本是v2： env：offline  
在本地git pull，提示有冲突。  
原因：远程代码库版本更新了一下v2；本地库还是原来的版本v1，那么git pull的时候发现本地和远程不是一个版本，那么就会拉取远程库的代码v2到本地v1，发现有冲突。
# 2.文件版本一致，没有冲突
本地文件host.conf，修改当前版本v1：port：8081  
线上host.conf， 版本是v1，无修改。  
在本地git pull，没有提示有冲突。  
git status查看，本次有文件修改。 
# 3.在项目的根目录和子目录，分别git pull是什么区别？
子目录git pull：只会pull当前目录吗？测试结论：不会。  
![](/images/git/git-child-pull.png)  
根目录git pull：会pull所有文件吗？测试结论：会的。  
![](/images/git/git-root-pull.png)


