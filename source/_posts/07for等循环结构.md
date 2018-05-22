---
title: 07for等循环结构
date: 2018-05-22 13:10:36
tags:
- 循环结构
category: shell
---
# 1.for 
## (1) i 遍历
>for i in 1 2 3 4  
do  
echo $i  
done  
或者：for i in ${1..10}、for i in ${1..10..3}

## (2)遍历文件列表
>for i  in $(ls)

## (3)遍历输入参数列表
>for i  in $@ 或者for i  in $*

## (4)遍历输入参数列表
>for args   #等同于for i  in $@  
do  
echo $args  
done

## (5)类c风格的for循环
>for ((x; xxx; xxx))  
do  
xxx  
done

# 2.while
>while [[  xxx ]]  
do  
something  
done