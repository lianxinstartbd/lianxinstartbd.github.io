---
title: 更换电脑后如何写blog
tags:
  - 更换电脑 hexo
date: 2018-05-22 15:24:31
category: next
---
## 1. 更换电脑后，如何更快的搭建好环境，直接写blog？  
参考知乎上的教程，有两种方案：  
+ 方案一：代码分为源文件和生成的静态文件。所有文件公用一个github的repo，创建分支 *`hexo`* 。  
&ensp;&ensp;&ensp;&ensp;源文件也就是source、theme、db和配置文件等，提交到分支 *`hexo`* 上。  
&ensp;&ensp;&ensp;&ensp;静态文件也就是最后生成public目录下的的html、images、js等文件，提交到 *`master`* 上。  
![](/images/machine.png)  
+ 方案二：用两个GitHub Repo，一个Repo放你Hexo的源文件（这里称之为Source Repo）  
&ensp;&ensp;&ensp;&ensp;另一个Repo放Hexo生成出来的静态网站（这里称之为Content Repo）  
&ensp;&ensp;&ensp;&ensp;然后使用AppVeyor做持续集成。每当需要更新博客，只需要更新Source Repo，AppVeyor会自动生成静态网站并push到Content Repo，一气呵成，版本控制完全由GitHub完成，也不需要手动deploy。  
&ensp;&ensp;&ensp;&ensp;但是ci工具AppVeyor目前只支持linux和windows，目前我使用的是mac，暂时先不尝试。
+ 综上考虑，使用方案一，将本地的源文件上传到hexo分支。

## 2. 继续写blog的最佳实践

+ git clone代码，切换到hexo分支
+ 执行hexo g，报错：   
ERROR Local hexo not found in ~/blogs/hexo   
ERROR Try running: 'npm install hexo —save'
   
   *`原因`* : hexo是使用npm安装的，安装之后的文件保存在 *`./node_modules`* ，由于配置文件 *`.gitignore`* 中设置的是不上传目录 *`./node_modules`* 下的文件 ，所以hexo可执行文件在git clone的代码中是没有的，所以报错：该目录没有找到可以执行的hexo。
   > .DS_Store   
   Thumbs.db   
   db.json   
   *.log   
   node_modules/   
   public/   
   .deploy*/

+ 需要使用npm进行安装，   
执行： npm install hexo   
+ 再次执行hexo g，hexo s，能够正常访问本地blog。
+ public目录也正确生成了。   
*`切记`* ：图片存放位置是hexo分支下的source/images中，执行hexo g之后，会自动存放到public下，在执行hexo d，会把public目录上传到git的master分支。
+ 最后在hexo分支下，上传source下新增的文件，也就是保存blog的源文件。   
所以，总结上述过程，更换电脑之后，只需要在一个目录下，操作两个步骤：
+ git clone，并且切换到hexo分支。
+ 依次执行下列指令：  
npm install hexo  

npm install、npm  
install hexo-deployer-git（记得，不需要hexo init这条指令）

## 2. 开发环境配置

## 3. 必备软件
+ git
+ chrome
+ xmind
+ visual studio code
+ pycharm
+ jmeter
+ charles
+ securecrt
+ beyond compare
+ postman
+ 
