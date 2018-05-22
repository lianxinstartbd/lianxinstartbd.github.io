---
title: 08nohup执行
tags:
  - nohup执行
date: 2018-05-22 14:20:56
category: shell
---
## 1.nohup sh xx &  
后台执行脚本xx，日志打在nohup.log中。
### 实例：nohup command > myout.file 2 >&1 &
异常日志打在 *`myout.file`* 文件中，“2”代表异常日志、错误日志，“&1”代表前面设置的myout.file文件。  
## 2.如果sh  xx，脚本正确执行，nohup不能正确执行，则要检查以下几点：
首先使用sh file.sh，尝试下文件是否可以单独被执行，解决语法问题以及逻辑问题，然后在使用nohup执行。
+ 是否有可执行权限，chmod  +x  xxx
+ nohup之前，source ~/.bash_profile
+ 通过报错日志或者打点来排查定位问题。