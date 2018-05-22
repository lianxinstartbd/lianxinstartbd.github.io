---
title: module安装方法
date: 2018-05-21 11:59:38
tags:
- module安装
category: python
---
# 方法1： 单文件模块
直接把文件拷贝到 $python_dir/Lib
# 方法2： 多文件模块，带setup.py
下载模块包，进行解压，进入模块文件夹，执行：  
python setup.py install
# 方法3：easy_install 方式
先下载ez_setup.py,运行python ez_setup 进行easy_install工具的安装，之后就可以使用easy_install进行安装package了。  
easy_install  packageName  
easy_install  package.egg
# 方法4：pip 方式 
先进行pip工具的安裝：easy_install pip（pip 可以通过easy_install 安裝，而且也会装到 Scripts 文件夹下。）  
安裝：pip install PackageName  
更新：pip install -U PackageName  
移除：pip uninstall PackageName  
搜索：pip search PackageName  
帮助：pip help  
# 包管理器原理
很多系统和语言都提供了包管理器。你可以把“包管理器”想象成一个类似应用商店的工具。Python 的包管理器里就是各种第三方模块。有了它，不用998，也不用98，只需要一条命令，就可以自动帮你下载并安装。

Python 常用的包管理器是 pip 和 easy_install。他们会从一个叫做 PyPI 的源里搜索你要的模块，找到后自动下载安装。PyPI 是 Python 官方的第三方模块仓库，供所有开发者下载或上传代码。

如果你用的是 Mac 或者 Linux，那么同 Python 一样，你的系统里应该自带了 pip。而如果你是 Windows，那么在安装 Python 的时候，勾选 pip 和 Add python.exe to Path，就会帮你同时安装好 pip 并设置好环境变量中的路径。如果无法使用 pip，确认 Python 安装目录下的 Scripts 子目录中有 pip，并且这个子目录的路径被加在了环境变量 Path 中。如果没有 pip，则要通过下载 setuptools 安装，或建议直接重新安装一遍 Python。  
注：虽然Python的模块可以拷贝安装，但是一般情况下推荐制作一个安装包，即写一个setup.py文件来安装。  
setup.py文件的使用如下:  
% python setup.py build     #编译  
% python setup.py install    #安装  
% python setup.py sdist      #制作分发包  
% python setup.py bdist_wininst    #制作windows下的分发包  
% python setup.py bdist_rpm  
## setup.py文件的编写
setup.py中主要执行一个 setup函数，该函数中大部分是描述性东西，最主要的是packages参数，列出所有的package，可以用自带的find_packages来动态获取package。所以setup.py文件的编写实际是很简单的。  
简单的例子:  
### setup.py文件：  
>from setuptools import setup, find_packages  
setup(  
&ensp;&ensp;name = " mytest " ,   
&ensp;&ensp;version = " 0.10 " ,  
&ensp;&ensp;description = " My test module " ,  
&ensp;&ensp;author = " Robin Hood " ,  
&ensp;&ensp;url = " http://www.csdn.net " ,  
&ensp;&ensp;license = " LGPL " ,  
&ensp;&ensp;packages = find_packages(),  
&ensp;&ensp;scripts = [ " scripts/test.py " ],  
&ensp;&ensp;)

### mytest.py
>import sys  
def get():  
&ensp;&ensp;return sys.path

### scripts/test.py
>import os  
print os.environ.keys() 

setup中的scripts表示将该文件放到 Python的Scripts目录下，可以直接用。OK，简单的安装成功，可以运行所列举的命令生成安装包，或者安装该python包。本机测试成功(win32-python25)！






