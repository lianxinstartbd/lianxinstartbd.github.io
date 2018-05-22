---
title: streaming相关设置
date: 2018-05-18 13:16:25
tags:
- hadoop    
- streaming
category: hadoop
---
1. -D 指定基于哪些key进行分桶  
基于指定的Key进行分桶，打标签  
指定列数:  
>-D num.key.fields.for.partition=1 # 只用1列Key做分桶   
-D num.key.fields.for.partition=2 # 使用1,2共两列key做分桶

指定某些字段做key  
>-D mapred.text.key.partitioner.option =-k1,2 # 第1,2列Key做分桶  
-D mapred.text.key.partitioner.option =-k2,2 # 第2列key做分桶

都要修改partition为能够只基于某些Key进行分桶的类  
>-partitioner org.apache.hadoop.mapred.lib.KeyFieldBasedPartitioner  

-D 指定将reducer的输出进行压缩
>-D mapred.output.compress=true -D mapred.output.compression.codec=org.apache.hadoop.io.compress.GzipCodec

-D 指定将mapper的输出进行压缩  
>-D mapred.compress.map.output=true -D mapred.map.output.compression.codec=org.apache.hadoop.io.compress.GzipCodec

更多参数设置参看：https://www.cnblogs.com/shay-zhangjin/p/7714868.html