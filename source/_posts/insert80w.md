---
title: insert80w
date: 2018-05-18 15:09:26
tags:
- mysql
- insert
category: mysql
---
1.使用sql语句，先insert数据，后进行update，1w条数据需要2h。  
2.先做一个测试：  
整备一个文件：756383行（75w+）  
insert整个文件看一下效率。 （shell中的sql命令） 
总耗时：7s。  
3.总结：  
在某些情况下，可以把要insert的数据保存到一个文件中，然后使用shell中的sql命令：  
"load data local infile '$result' ignore into table eagleeye.db_test Fields Terminated By ' ';"