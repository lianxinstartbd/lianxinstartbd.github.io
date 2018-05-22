---
title: hexo工作原理
date: 2018-05-16 06:34:28
tags:
 - Hexo
 - 工作原理
 - blog
 - 搭建
categories: hexo+github 
---
### hexo与github pages之间的原理？ 
【hexo简介】
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。  
【hexo目录】  
-rw-r--r--    1 wangqun02  INTERNAL\Domain Users   1858  5 10 17:08 _config.yml // 站点配置文件  
-rw-r--r--    1 wangqun02  INTERNAL\Domain Users    174  5 14 08:30 db.json // 缓存文件  
drwxr-xr-x  254 wangqun02  INTERNAL\Domain Users   8636  5 10 16:41 node_modules // 安装的插件以及hexo所需的一些nodejs模块  
-rw-r--r--    1 wangqun02  INTERNAL\Domain Users  95026  5 10 16:41 package-lock.json   
-rw-r--r--    1 wangqun02  INTERNAL\Domain Users    483  5 10 16:41 package.json // 项目的依赖文件  
drwxr-xr-x   12 wangqun02  INTERNAL\Domain Users    408  5 10 17:19 public  
drwxr-xr-x    5 wangqun02  INTERNAL\Domain Users    170  5 10 16:12 scaffolds // 模版文件  
drwxr-xr-x    4 wangqun02  INTERNAL\Domain Users    136  5 10 17:19 source // 源文件，用来存放你的文章 md 文件  
drwxr-xr-x    4 wangqun02  INTERNAL\Domain Users    136  5 10 17:07 themes // 主题文件  
【工作原理】  
hexo g：将我们的blog内容和使用的主题相结合生成静态文件的过程。会遍历主题文件中的 source 文件夹（js、css、img 等静态资源），然后建立索引，然后根据索引生成 pubild 文件夹中，此时的 publid 文件是由 html、 js、css、img 建立的纯静态文件，存放在public中，按照时间年、月、日、blog名称递归创建目录，最深目录中的文件是index.html，就是每篇blog的静态文件。  
hexo d：部署文件。部署主要是根据在 _config.yml 中配置的 git 仓库或者其他地址，将 public 文件上传至 github 或者其他中。然后再根据上面的 github 提供的 pages 服务呈现出页面。当然你也可以直接将你生成的 public 文件上传至你自己的服务器上（比如自己购买的虚拟主机）。  
【Hexo模板引擎】  
模板引擎的作用，就是将界面与数据分离。最简单的原理是将模板内容中指定的地方替换成数据，实现业务代码与逻辑代码分离。  
我们可以注意到，在 Hexo 中，source 文件夹和 themes 文件夹是在同级的，我们就可以将 source 文件夹理解为数据库，而主题文件夹相当于 界面。然后我们 hexo g 就将我们的数据和界面相结合生成静态文件 public。  
Hexo 的模板引擎是默认使用 ejs 编写的。hexo首先会解析 md 文件，然后根据 layout 判断布局类型，再调用其他的文件，这样每一块的内容都是独立的，提高代码的复用性。最终会生成一个 html 页面。  
【hexo与github page的关系】  
参考：http://coderunthings.com/2017/08/20/howhexoworks/  
![](/images/hexo-git/hexo-git.png)   