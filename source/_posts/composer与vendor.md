---
title: composer与vendor
date: 2018-05-18 18:09:54
tags:
- composer
- vendor
category: php
---
# 1.composer
又称为： *`中国全量镜像`* 。  
对于现代语言而言，包管理器基本上是标配。Java 有 Maven，Python 有 pip，Ruby 有 gem，Nodejs 有 npm。PHP 的则是 PEAR，不过 PEAR 坑不少。  
php托管于git上，所有有时候下载第三方库或者插件，会受到影响，所以在中国搞了一个全量镜像服务器。  
你可以在自己的项目中声明所依赖的外部工具库（libraries），Composer 会帮你安装这些依赖的库文件。  
# 2.vendor  
vendor是第三方库和插件放置的文件夹，一般来源于composer的安装。下载下来的文件都会放到这个文件里。  
# 3.使用  
1. 下载安装之后，可以将composer.phar放到系统路径下  
2. 进入到当前项目路径，保证项目路径下有composer.json（项目所依赖的库文件），内容例如：需要依赖的库以及版本信息  
![](/images/php/php-01.png)  
3. 首次下载，则使用：composer install，下载后的文件放到vendor文件夹中。  
4. 自动加载.除了库的下载，Composer 还准备了一个自动加载文件，它可以加载 Composer 下载的库中所有的类文件。使用它，你只需要将下面这行代码添加到你项目的引导文件中：  
  require 'vendor/autoload.php';  
# 4.composr.lock
在安装依赖后，Composer 将把安装时确切的版本号列表写入 *`composer.lock`* 文件。*`这将锁定改项目的特定版本`*。   
请提交你应用程序的 composer.lock （包括 composer.json）到你的版本库中  
这是非常重要的， *`因为 install 命令将会检查锁文件是否存在，如果存在，它将下载指定的版本（忽略 composer.json 文件中的定义）`*。  
这意味着，任何人建立项目都将下载与指定版本完全相同的依赖。你的持续集成服务器、生产环境、你团队中的其他开发人员、每件事、每个人都使用相同的依赖，从而减轻潜在的错误对部署的影响。即使你独自开发项目，在六个月内重新安装项目时，你也可以放心的继续工作，即使从那时起你的依赖已经发布了许多新的版本。  
 *`如果不存在 composer.lock 文件，Composer 将读取 composer.json 并创建锁文件`* 。  
 这意味着如果你的依赖更新了新的版本，你将不会获得任何更新。 *`此时要更新你的依赖版本请使用 update 命令`* 。这将获取最新匹配的版本（根据你的 composer.json 文件）并将新版本更新进锁文件。  
  *`composer update`*  
如果只想安装或更新一个依赖，你可以白名单它们：
 *`composer update monolog/monolog [...]`* 



