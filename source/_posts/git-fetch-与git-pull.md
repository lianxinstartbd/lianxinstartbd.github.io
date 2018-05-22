---
title: git fetch 与git pull
date: 2018-05-17 15:31:17
tags:
- git fetch      
- git pull
category: git
---
# Git中从远程的分支获取最新的版本到本地有这样2个命令：
## git fetch：相当于是从远程获取最新版本到本地，不会自动merge
 
 git fetch origin master  
 git log -p master..origin/master  
 git merge origin/master  
 以上命令的含义：  
 首先从远程的origin的master主分支下载最新的版本到origin/master分支上  
 然后比较本地的master分支和origin/master分支的差别  
 最后进行合并  
 上述过程其实可以用以下更清晰的方式来进行：  
 git fetch origin master:tmp  
 git diff tmp  
 git merge tmp
 
从远程获取最新的版本到本地的test分支上，之后再进行比较合并  
## git pull：相当于是从远程获取最新版本并merge到本地  
git pull origin master  
上述命令其实相当于git fetch 和 git merge  
在实际使用中，git fetch更安全一些  
因为在merge前，我们可以查看更新情况，然后再决定是否合并


