---
title: post四种请求格式
date: 2018-05-16 06:59:37
tags:
- http       
- post  
category: http
---
# 0.前言  
----
HTTP 协议是以 ASCII 码传输，建立在 TCP/IP 协议之上的应用层规范。规范把 HTTP 请求分为三个部分：状态行、请求头、消息主体。类似于下面这样：  
>&lt;method> &lt;equest-URL>&lt;version>  
>&lt;headers>  
>&lt;entity-body>  

协议规定 POST 提交的数据必须放在消息主体（entity-body）中，但协议并没有规定数据必须使用什么编码方式。实际上，开发者完全可以自己决定消息主体的格式，只要最后发送的 HTTP 请求满足上面的格式就可以。   
但是，数据发送出去，还要服务端解析成功才有意义。一般服务端语言如 php、python 等，以及它们的 framework，都内置了自动解析常见数据格式的功能。  
服务端通常是根据 *`请求头（headers）中的Content-Type字段`* 来获知请求中的消息主体是用何种方式编码，再对主体进行解析。所以说到 POST 提交数据方案，包含了 Content-Type 和消息主体编码方式两部分。  
# 1.json格式
----
JSON 格式支持比键值对复杂得多的结构化数据，这一点也很有用，可以支持的数据结构非常深。  
## 请求参数格式：  
Google 的 AngularJS 中的 Ajax 功能，默认就是提交 JSON 字符串。例如下面这段代码：  
>var data = {'title':'test', 'sub' : [1,2,3]};  
>$http.post(url, data).success(function(result) {    
    ...
>});  

最终发送的请求是：  
>POST http://www.example.com HTTP/1.1  
>Content-Type: application/json;charset=utf-8  
>{"title":"test","sub":[1,2,3]}     
 
这种方案，可以方便的提交复杂的结构化数据，特别适合 RESTful 的接口。各大抓包工具如 Chrome 自带的开发者工具、Firebug、Fiddler，都会以树形结构展示 JSON 数据，非常友好。  
但也有些服务端语言还没有支持这种方式，例如 php 就无法通过 $_POST 对象从上面的请求中获得内容。  
这时候，需要自己动手处理下：在请求头中 Content-Type 为 application/json 时，从 php://input 里获得原始输入流，再 json_decode 成对象。一些 php 框架已经开始这么做了。  
# 2.form表单
-----
浏览器的原生 &lt;form> 表单，如果不设置 enctype 属性，那么最终就会以 application/x-www-form-urlencoded 方式提交数据，例如：  
+ 请求参数格式：  
![](/images/http/post-01.png)  
提交的数据按照 *`key1=val1&key2=val2`* 的方式进行编码，key 和 val 都进行了 *`URL`* 转码。大部分服务端语言都对这种方式有很好的支持。例如 PHP 中，$_POST['title'] 可以获取到 title 的值，$_POST['sub'] 可以得到 sub 数组。
参数列表为：  
![](/images/http/post-02.png)  
data对应的value为一个json格式：  
![](/images/http/post-03.png)  
最终这个参数列表被编码为一个 *`字符串数据`*：data=xxxx，charles中会看到这样：  
![](/images/http/post-04.png)  
很多时候，我们用Ajax提交数据时，也是使用这种方式。例如 JQuery 和 QWrap 的 Ajax，Content-Type 默认值都是「application/x-www-form-urlencoded;charset=utf-8」。
+ 返回值格式json：  
![](/images/http/post-05.png)  
+ 发送请求的代码：
>#首先构造参数，例如  
with open(image_file) as f:  
image_base64 = base64.b64encode(f.read())  
#data: 是一个dict ，不是json  
data = {  
&ensp;&ensp;'image': image_base64,  
&ensp;&ensp;'type': 'CHARS',  
&ensp;&ensp;'LANG': 'CHN',  
}  
#先把value中的dict格式参数列表进行json编码，就变成json格式字符  
data_string = json.dumps(data)  
#print data_string  
#{"LANG": "CHN", "image": agdagvcaxxae13asga, "type": "CHARS"  
values = {    
&ensp;&ensp;"BAIDULOC": "12936521_4580521_1000_149_1383542366651",  
&ensp;&ensp;"data": data_string #json字符串作为data的value  
}  
#url编码  
params = urllib.urlencode(values)  
#print params  
#BAIDULOC=12936521_4580521_1000_149_1383542366651&data=%7B%22LANG%22%3A+%22CHN%22%2C+%22image%22%3A+%22test%22%2C+%22type%22%3A+%22CHARS%22%  

# 3.multipart上传文件
-----
使用表单上传文件时，必须让 &lt;form> 表单的 enctype 等于 multipart/form-data，也是浏览器原生支持的。使用charles抓包得到详情数据，例如：  
![](/images/http/post-06.png)  
+ 请求参数格式：  
![](/images/http/post-07.png)  
参数列表为：  
![](/images/http/post-08.png)  
+ 返回值格式json：  
返回值格式是由header中的accpet值来进行匹配。  
![](/images/http/post-10.png)  
所以这里返回的是json，是合理的。  
![](/images/http/post-11.png)  
+ 发送请求的代码：  
>需要安装python的poster模块：pip  install poster即可。    
from poster.encode import multipart_encode  
from poster.streaminghttp import register_openers  
def multi_post_http():  
&ensp;&ensp;image_file = self.cur_file_dir() +  '/testdata/jay.jpg'  
&ensp;&ensp;image_base64 = ""  
&ensp;&ensp;with open(image_file) as f:  
&ensp;&ensp;&ensp;&ensp;image_base64 = base64.b64encode(f.read())  
&ensp;&ensp;#按照json格式组装参数列表  
&ensp;&ensp;data = {  
    &ensp;&ensp;&ensp;&ensp;"image" : image_base64,  
    &ensp;&ensp;&ensp;&ensp;"from": "wiseforapi",  
    &ensp;&ensp;&ensp;&ensp;"apiname": "whitevalentineact"  
    &ensp;&ensp;}   
    &ensp;&ensp;url = "https://graph.baidu.com/upload?tn=weixin&_=1521030027084"  
    &ensp;&ensp;register_openers()  
    &ensp;&ensp;按照multipart格式处理参数得到header和参数  
    &ensp;&ensp;datagen, re_headers = multipart_encode(data)  
    &ensp;&ensp;try:  
    &ensp;&ensp;&ensp;&ensp;request = urllib2.Request(url, datagen, re_headers)  
    &ensp;&ensp;&ensp;&ensp;result = urllib2.urlopen(request)  
    &ensp;&ensp;&ensp;&ensp;data = result.read()  
    &ensp;&ensp;except URLError as e:  
    &ensp;&ensp;&ensp;&ensp;errinfo += path + ' request error:{}'. format(e) + '\n'  
    &ensp;&ensp;return False, errinfo

# 4.text/xml
它是一种使用 HTTP 作为传输协议，XML 作为编码方式的远程调用规范。典型的 XML-RPC （XML Remote Procedure Call）请求是这样的：  
![](/images/http/post-12.png)  
XML-RPC 协议简单、功能够用，各种语言的实现都有。  
它的使用也很广泛，如 WordPress 的 XML-RPC Api，搜索引擎的 ping 服务等等。  
JavaScript 中，也有现成的库支持以这种方式进行数据交互，能很好的支持已有的 XML-RPC 服务。不过，我个人觉得 XML 结构还是过于臃肿，一般场景用 JSON 会更灵活方便。


