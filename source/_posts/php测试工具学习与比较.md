---
title: php测试工具学习与比较
date: 2018-05-20 10:58:29
tags:
- 测试工具
category: php
---
1.phpunit：测试框架，xunit中的一员  
2.xdebug：debug工具  
3.php-code-coverage：应用于hhvm的代码覆盖率统计工具，能够收集、生成、展示覆盖率报告。  
三者关系： 最新的phpunit基于PHP_CodeCoverage（目前最新版本是2.1），而PHP_CodeCoverage又基于Xdebug。    
4.patest：qa维护的测试工具  
5.phptest：又称为PTest，是odp自带的测试框架，基于phpunit封装。  
6.支持路径覆盖率的vendor包：
要求： php-xdebug.tar.gz包含了php（5.6.19，需求>5.6）、xdebug(2.3.3  需求>=2.1)、以及用phar打包好的phpunit(5.2.9【其中包含经过改装的php_codeCoverage】，需求=5.2.9)。  
待调研：odp的php是否能升级到5.6？    php-code-coverage工具，是否需要升级xdebug和phpunit，因为hhvm3.0.1已经实现了xdebug的覆盖率统计接口api。


