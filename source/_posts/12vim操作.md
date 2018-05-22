---
title: 12vim操作
tags:
  - vim操作
date: 2018-05-22 14:45:06
category: shell
---
# 查看字符编码
## 1.在Vim中可以直接查看文件编码
命令模式： *`:set fileencoding`*   
即可显示文件编码格式。  
## 2.设置文件编码格式
如果你只是想查看其它编码格式的文件或者想解决用Vim查看文件乱码的问题，那么你可以在 *`~/.vimrc`* 文件中添加以下内容：  
>set&ensp;encoding=utf-8&ensp;fileencodings=ucs-bom,utf-8,cp936

这样，就可以让vim自动识别文件编码（可以自动识别UTF-8或者GBK编码的文件），其实就是依照 fileencodings提供的编码列表尝试，如果没有找到合适的编码，就用latin-1(ASCII)编码打开。
# 文件编码转换
## 1.在Vim中直接设置文件编码,比如将一个文件转换成utf-8格式
命令模式：*`:set fileencoding=utf-8`* 
## 2. enconv 转换文件编码
比如要将一个GBK编码的文件转换成UTF-8编码，操作如下:  
>enconv -L zh_CN -x UTF-8 filename

## 3. iconv 转换
iconv的命令格式如下：  
>iconv -f encoding -t encoding inputfile

比如将一个UTF-8 编码的文件转换成GBK编码:
>iconv -f UTF-8 -t GBK file1 -o file2

# vim中查看格式详情
命令模式： *`:set list`*   
 *`python文件中关于空格缩进等问题，通过这个命令就可以看出来`* .