---
title: python_path
date: 2018-05-21 12:09:14
tags:
- python_path
category: python
---
# 1.检查当前的path
>[GCC 4.6.3] on linux  
python  
Type "help", "copyright", "credits" or "license" for more information.  
\>\>\> import sys  
\>\>\> sys.path  
['', '/usr/local/Python-3.4.0/lib/python3.4/site-packages/setuptools-5.4.1-py3.4.egg', '/usr/local/Python-3.4.0/lib/python34.zip', '/usr/local/Python-3.4.0/lib/python3.4', '/usr/local/Python-3.4.0/lib/python3.4/plat-linux', '/usr/local/Python-3.4.0/lib/python3.4/lib-dynload', '/usr/local/Python-3.4.0/lib/python3.4/site-packages']   

sys.path包含了一个Python解释器自动查找所需模块的路径的列表。注意列表中的第一个字符串是空的，这说明当前目录也是sys.path中的一部份，环境变量PYTHONPATH也一样。这说明你可以在程序中引入当前目录中的模块。 
# 2.环境变量pythonpath 
在文件～/.bash_profile中，设置如下：
>export  
PYTHONPATH=/home/work/module/vs_dqc:/home/work/module/vs_dqc/thirdlib:$PYTHONPATH

那么python代码在执行过程中会查找这个目录，导入import的module.
# 3.通过建立.pth文件方式
在python3.4的site-packages文件夹下中创建 .pth文件，然后将需要添加的路径写到.pth文件中去，pth文件也可以使用注释，如下：
>cd /usr/local/Python-3.4.0/lib/python3.4/site-packages    //这个文件夹也是pyhton模块安装的地方  
sudo nano pythonpathdelf.pth  
#.pth file for the my project(这行是注释)  
/usr/lib/pyshared/python2.7/smbus.so  
/usr/lib/python2.7/dist-packages/smbus-1.1.egg-info  
/usr/lib/python2.7/dist-packages/smbus.so  
/usr/share/pyshared/smbus-1.1.egg-info  
/usr/local/src/i2c-tools-3.1.1/py-smbus/smbusmodule.c

# 4.设置临时的path  
linux：在执行相关pyt文件时，首先执行export PYTHONPATH=/home/work/module/vs_dqc:/home/work/module/vs_dqc/thirdlib:$PYTHONPATH，将自己需要的路径放进去，然后执行python  xxx.py  
临时放进去的路径也能找到，只是临时有效。
# 5.代码中使用相对路径
在py文件中，使用如下代码：
>import sys  
import os  
sys.path.append(os.path.dirname(os.path.realpath(__file__)) + '/../../selenium_test')





