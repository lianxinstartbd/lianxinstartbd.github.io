---
title: copy
date: 2018-05-21 10:36:49
tags:
- copy两种
category: python
---
我们寻常意义的复制就是 *`深复制`* ，即将 *`被复制对象`* 完全再复制一遍作为独立的新个体单独存在。所以改变原有被复制对象不会对已经复制出来的新对象产生影响。  
而 *`浅复制`* 并不会产生一个独立的对象单独存在，他只是将原有的数据块打上一个新标签，所以当其中一个标签被改变的时候，数据块就会发生变化，另一个标签也会随之改变。这就和我们寻常意义上的复制有所不同了。  
对于不同的数据类型， *`复制`* 的含义也不同。  
1. 对于简单的 object，用 shallow copy 和 deep copy 没区别。
2. 复杂的 object（ *`引用类型`* ）， 如 list 中套着 list 的情况，shallow copy 中的 子list，并未从原 object 真的「独立」出来。也就是说，如果你改变原 object 的子 list 中的一个元素，你的 copy 就会跟着一起变。这跟我们直觉上对「复制」的理解不同。  
![](/images/python/python-01.png)  
如果要使得引用类型的变量深复制，则需要使用：  
cop2 = copy.deepcopy(origin)  
![](/images/python/python-02.png)