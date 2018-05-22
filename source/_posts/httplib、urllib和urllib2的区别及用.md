---
title: httplib、urllib和urllib2的区别及用
date: 2018-05-21 11:38:57
tags:
- httplib、urllib和urllib2
category: python
---
# urllib和urllib2
urllib 和urllib2都是接受URL请求的相关模块，但是urllib2可以接受一个Request类的实例来设置URL请求的headers，urllib仅可以接受URL，这意味着，你不可以伪装你的User Agent字符串等。  
urllib提供urlencode方法用来GET查询字符串的产生，而urllib2没有。这是为何urllib常和urllib2一起使用的原因。  
目前的大部分http请求都是通过urllib2来访问的。  
## 1. urllib简单用法  
### urllib.urlopen(url[, data[, proxies]]) :  
>google = urllib.urlopen('http://www.google.com')  
print 'http header:/n', google.info()  
print 'http status:', google.getcode()  
print 'url:', google.geturl()  
for line in google: # 就像在操作本地文件  
&ensp;&ensp;print line  
google.close()  

## 2. urllib2简单用法
### 最简单的形式
>import urllib2
    response=urllib2.urlopen('http://www.douban.com'，timeout = 1) //超时设置  
    html=response.read()
### 实际步骤：
+ urllib2.Request()的功能是构造一个请求信息，返回的req就是一个构造好的请求
+ urllib2.urlopen()的功能是发送刚刚构造好的请求req，并返回一个文件类的对象response，包括了所有的返回信息。
+ 通过response.read()可以读取到response里面的html，通过response.info()可以读到一些额外的信息。  

代码如下：
>#!/usr/bin/env python  
import urllib2  
req = urllib2.Request("http://www.douban.com")  
response = urllib2.urlopen(req)  
html = response.read()  
print html

有时你会碰到，程序也对，但是服务器拒绝你的访问。这是为什么呢?问题出在请求中的头信息(header)。 有的服务端有洁癖，不喜欢程序来触摸它。这个时候你需要将你的程序伪装成浏览器来发出请求。请求的方式就包含在header中。
常见的情形：
>import urllib  
import urllib2  
url = 'http://www.someserver.com/cgi-bin/register.cgi'  
user_agent = 'Mozilla/4.0 (compatible; MSIE 5.5; Windows NT)'   #将user_agent写入头信息  
values = {'name' : 'who','password':'123456'}  
headers = { 'User-Agent' : user_agent }  
data = urllib.urlencode(values)  
req = urllib2.Request(url, data, headers)  
response = urllib2.urlopen(req)  
the_page = response.read()  

## 3. urllib2带cookie的使用
>#coding:utf-8
import urllib2,urllib  
import cookielib  
url = r'http://www.renren.com/ajaxLogin'  
#创建一个cj的cookie的容器  
cj = cookielib.CookieJar()  
opener = urllib2.build_opener(urllib2.HTTPCookieProcessor(cj))  
#将要POST出去的数据进行编码  
data = urllib.urlencode({"email":email,"password":pass})  
r = opener.open(url,data)  
print cj

# httplib  
httplib实现了HTTP和HTTPS的客户端协议，一般不直接使用，在更高层的封装模块中（urllib,urllib2）使用了它的http实现。  
## 简单示例
>#!/usr/bin/env python    
#-*- coding: utf-8 -*-    
import httplib  
import urllib    
def sendhttp():  
&ensp;&ensp;data = urllib.urlencode({'@number': 12524, '@type': 'issue', '@action': 'show'})     
&ensp;&ensp;headers = {"Content-type": "application/x-www-form-urlencoded",  
               "Accept": "text/plain"}  
&ensp;&ensp;conn = httplib.HTTPConnection('bugs.python.org')  
&ensp;&ensp;conn.request('POST', '/', data, headers)  
&ensp;&ensp;httpres = conn.getresponse()  
&ensp;&ensp;print httpres.status  
&ensp;&ensp;print httpres.reason  
&ensp;&ensp;print httpres.read()             
if __name__ == '__main__':    
&ensp;&ensp;sendhttp()  

