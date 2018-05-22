---
title: Hexo+GitHub Pages=Hello World
date: 2018-05-11 11:53:30
tags:
 - Hexo
 - Github pages
 - blog
 - 搭建
categories: hexo+github 
---
## 这篇文章记录下blog的搭建过程以及遇到的问题
blog搭建过程首先是参考了网上的很多教程，了解下目前都是采用什么工具编写、文件存储以及域名申请等。
### 域名申请
使用的是阿里云服务 
### Hexo+Github Pages 
模版使用hexo，文件存储使用github pages。  
自己使用的是mac本，首先安装nodejs和hexo，安装过程参考教程即可： https://blog.csdn.net/u011974987/article/details/51331822。   
hexo安装完成之后，创建一个blog目录，执行“hexo init 目录名”，则初始化了一个blog的目录，继续安装教程安装，执行“hexo g”，生成了静态页面，最后执行“hexo s”，启动起hexo，打开默认的url，即可看到默认的hello world页面。  
接着，将hexo生成的blog存储到github pages上。首先注册github账号，并且创建新的仓库，仓库的路径一定是：xxx.github.io，必须使用github的用户名，刚开始看教程时没明白这个意思，使用自定义的名字，结果发现是一个普通的代码库。每个帐号只能有一个仓库来存放个人主页，而且仓库的名字必须是username/username.github.io，这是特殊的命名约定。你可以通过http://username.github.io 来访问你的个人主页。接着安装git包：npm install hexo-deployer-git --save。 
最后，修改blog目录中的hexo的配置文件_config.yml，修改【部署配置】：  
deploy:  
  type: git  
    repo: git@github.com:lianxinstartbd/lianxinstartbd.github.io.git  
    branch: master  
其中注意【repo】项，参考网上教程的设置，一直不成功，根据提示信息以及其他网友的评论，才找到如上的最佳实践。最后，执行hexo d，blog就提交到github上了，打开GitHub pages的页面，能点击仓库名称跳转到blog页面，且在仓库中能看到文件列表，说明部署成功。  
### hexo风格  
默认的风格是landscape，这里我选择了使用人数最多的也是自己喜欢的next主题风格。  
对于“next”，对于现在的我也有很多含义。  
1. next work
2. next stage
3. next myself
4. jobs也创办过next啊  
  
哈哈，从git上下载了next的包，存放到目录/blog/themes下，并且修改了配置文件_config.yml：  
theme: next  
记住，每次在目录下修改，都要依次执行“hexo g”，“hexo d”，才能生成最新的静态文件并上传至git，此时刷新git pages，就能看到新的主题生效了。  
### 绑定域名  
这个过程按照上面博客步骤操作即可。  


 


