---
title: redis相关
date: 2018-05-21 17:47:47
tags:
- redis
category: redis
---
1. 测试redis，登录：  
>redis-cli -h ip -p port -n db的id  
例如：  
>redis-cli -h 10.95.39.53 -p 6379 -n 10
2. 批量删除批量删除keys：  
>redis-cli -h ip -p port -n 10 keys '正则匹配符'|xargs redis-cli -h 10.95.39.53 -p 6379 -n 10  del  
3. 通配符筛选key:  
>keys xxx*  

4. 删除通配符keys：  
>delete  xxx*

5. 全部删除：
>flushdb