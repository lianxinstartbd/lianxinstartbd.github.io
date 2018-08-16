---
title: 01thrift初体验
tags:
  - thrift初体验 mac intellij
date: 2018-08-16 11:10:25
category: thrift
---
项目中用到了thrift框架，自己按照网友的教程尝试了一把，这里记录下过程。   
### intellij安装thrift插件   
在preference中查找plugins，查找thrift，安装，重启即可。   
如果下载不下来，则需要手动去官网下载，在intellij里选择从disk中安装。其他插件安装过程类似。
### 新建一个maven项目，配置thrift相关
设置当前project settings的facets，添加“thrift”,主要是设置thrift compile之后的文件输出目录，如图：   
![](/images/thrift/thriftfacets.png)    
### 编写Hello.thrift文件: Hello.thrift
```
namespace java com.thrift.demo.service

service Hello{

    string helloString(1:string para)
    i32 helloInt(1:i32 para)
    bool helloBoolean(1:bool para)
    void helloVoid()
    string helloNull()
}
```
在此文件上右键，recompile “Hello.thrift”，输出目录则会生成相应的java源文件，如下：
![](/images/thrift/Hellointer.png) ps：将thrift文件编译为java文件的过程，可以本地安装thrift，使用thrift的命令进行。
>brew install thrift
thrift -gen java Hello.thrift
### 将生成的java文件复制到maven项目的src目录下，遇到几个问题：
1. 目录不匹配的情况，如下：
![](/images/thrift/direrror.png) 解决方法：   
使用快捷键，alt+enter，调起目录选择正确的目录即可。
2. override语法不识别，提示：override is not allowed when implementing interface method。   
解决方法：   
Project Settings > Modules > project_name > Language level)，选择6—overrided.
![](/images/thrift/language.png) 

### 配置maven项目的pom.xml，添加thrift依赖
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>ThriftAPI</groupId>
    <artifactId>ThriftAPI</artifactId>
    <version>1.0-SNAPSHOT</version>

    <dependencies>
        <dependency>
            <groupId>org.apache.thrift</groupId>
            <artifactId>libthrift</artifactId>
            <version>0.11.0</version>
        </dependency>
    </dependencies>
</project>
```

### 编写thrift接口的实现类HelloServiceImpl
```
  package com.thrift.demo.service;

  import org.apache.thrift.TException;

  public class HelloServiceImpl implements Hello.Iface {

    @Override
    public boolean helloBoolean(boolean para) throws TException {
        return para;
    }

    @Override
    public int helloInt(int para) throws  TException{
        try {
            Thread.sleep(20000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        return para;
    }

    @Override
    public String helloNull() throws  TException{
        return null;
    }


    @Override
    public String helloString(String para) {
        return para;
    }

    @Override
    public void helloVoid() {
        System.out.println("hello world");
    }

}```
### 编写HelloServiceServer类
```
package com.thrift.demo.service;

import org.apache.thrift.TProcessorFactory;
import org.apache.thrift.protocol.TBinaryProtocol;
import org.apache.thrift.server.TNonblockingServer;
import org.apache.thrift.server.TServer;
import org.apache.thrift.transport.TFramedTransport;
import org.apache.thrift.transport.TNonblockingServerSocket;
import org.apache.thrift.transport.TTransportException;

public class HelloServiceServer {


    public static void main(String[] args){
        try {
            TNonblockingServerSocket socket = new TNonblockingServerSocket(7911);
            Hello.Processor processor = new Hello.Processor(new HelloServiceImpl());
            TNonblockingServer.Args arg = new TNonblockingServer.Args(socket);
            arg.protocolFactory(new TBinaryProtocol.Factory());
            arg.transportFactory(new TFramedTransport.Factory());
            arg.processorFactory(new TProcessorFactory(processor));
            TServer server = new TNonblockingServer(arg);
            server.serve();
        } catch (TTransportException e) {
            e.printStackTrace();
        }
    }
}```
### 编写HelloServiceClient类
```
package com.thrift.demo.service;

import org.apache.thrift.protocol.TBinaryProtocol;
import org.apache.thrift.protocol.TProtocol;
import org.apache.thrift.transport.TFramedTransport;
import org.apache.thrift.transport.TSocket;
import org.apache.thrift.transport.TTransport;

public class HelloServiceClient {
    public static void main(String[] args){
        try {
            TTransport tTransport = getTTransport();
            TProtocol protocol = new TBinaryProtocol(tTransport);
            Hello.Client client = new Hello.Client(protocol);
            String result = client.helloString("hello");
            System.out.println("The result is: " + result);
        }catch (Exception e) {
            e.printStackTrace();
        }
    }

    private static TTransport getTTransport() throws Exception{
        try{
            TTransport tTransport = getTTransport("127.0.0.1", 7911, 5000);
            if(!tTransport.isOpen()){
                tTransport.open();
            }
            return tTransport;
        }catch(Exception e){
            e.printStackTrace();
        }
        return null;
    }

    private static TTransport getTTransport(String host, int port, int timeout) {
        final TSocket tSocket = new TSocket(host, port, timeout);
        final TTransport transport = new TFramedTransport(tSocket);
        return transport;
    }
}
```
### 代码目录为：
![](/images/thrift/projectdir.png)
### 启动HelloServiceServer，然后启动HelloServiceClient，client会得到如下结果：
![](/images/thrift/result.png)