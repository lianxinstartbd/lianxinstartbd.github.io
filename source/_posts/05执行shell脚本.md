---
title: 05执行shell脚本
date: 2018-05-10 16:53:00
tags:
- 执行shell脚本
category: shell
---
# 执行shell脚本的三种方式
## 1. sh  file
调用shell子进程，在shell解释器里执行file，用户要有file的读权限即可。

## 2. ./file  
将这个文件当作参数传递给shell子进程，用户要有file的x权限，且file中第一行要指定要 *`使用的shell解析器`* 。
>#！／bin/bash

## 3. source file
在当前的shell进程里解释执行file，脚本里所创建的所有变量都会保存到当前的shell里面。  
# shell脚本执行完成，退出状态：
成功：0

失败：非0

可以使用exit  xxx来强制返回状态值。

shell脚本中可以是$?来判断程序的退出状态是什么。