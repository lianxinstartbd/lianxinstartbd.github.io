---
title: http服务器
date: 2018-05-21 15:42:34
tags:
- http服务器
category: python
---
Python内置了一个简单的HTTP服务器，只需要在命令行下面敲一行命令，一个HTTP服务器就起来了：  
>python -m SimpleHTTPServer 80

后面的80端口是可选的，不填会采用缺省端口8000。注意，这会将当前所在的文件夹设置为默认的Web目录，试着在浏览器敲入本机地址：
>http://localhost:80

如果当前文件夹有index.html文件，会默认显示该文件，否则，会以文件列表的形式显示目录下所有文件。这样已经实现了最基本的文件分享的目的，你可以做成一个脚本，再建立一个快捷方式，就可以很方便的启动文件分享了。如果有更多需求，完全可以根据自己需要定制，具体的请参见官方文档SimpleHTTPServer，或者直接看源码。  
用于搭建http server的模块有如下三种：  
1）BaseHTTPServer：提供基本的Web服务和处理器类，分别是HTTPServer及BaseHTTPRequestHandler；  
2）SimpleHTTPServer：包含执行GET和HEAD请求的SimpleHTTPRequestHandler类；  
3）CGIHTTPServer：包含处理POST请求和执行的CGIHTTPRequestHandler类。  