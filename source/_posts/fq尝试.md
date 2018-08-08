---
title: fq尝试
tags:
  - fq
date: 2018-08-08 16:05:06
category: fq
---
之前关于fq，陆续使用过自由门等软件，最近学会了使用vps+vpn的方式fq，这里进行一个过程总结。   
# 准备工作 ：  
1. vps
2. shadowsocks   

# 操作步骤 ：  
## 1. 申请vps。   
使用的是vultr，平台地址：https://www.vultr.com/   
+ 注册一个账号，登陆进来，界面如下，可以选择os、mem、disk、software等。   
![](/images/fq/vultrindex.png)
+ 比如：选择ubuntu、openvpn、1G、location等参数，点击创建，则启动一个server，会分配相应的ip、root密码、openvpn的账户和密码等。

## 2. shadowsocks安装。   
+ 简介: shadowsocks是一个著名的轻量级socket代理，基于python编写。   
+ 工作模式: C/S模式。   
+ server端配置   
（1）使用root账号登陆vps上启动成功的server， 安装server，需要使用root权限。   
> apt-get update   
apt-get install -y python-pip   
pip install shadowsocks   

  （2）此时系统会多出来两个程序：
>/usr/bin/ssserver   
/usr/bin/sslocal

  （3）查看命令帮助:
> ssserver -h

 （4）可以得知，需要一个config文件，在一个目录下创建config.json文件，内容如下：
> #注释版配置   
{   
  "server":"servier_ip",     # 服务器IP   
  "server_port":65432,      # ss服务器所使用的端口号，建议改到30000-60000   
  "password":"password",    # ss服务器密码，轻易不要分享   
  "timeout":60,             # 超时时间，建议设置为60   
  "method":"rc4-md5"          # 加密方式，需要和客户端配合设置   
  }

 （5）执行命令，运行server，观察日志，是否能够正常启动
> ssserver -c config.json -f /tmp/ss.pid

 （6）如果能正常fq，则可以把server的启动脚本增加到 *`开机脚本`* 中：
 > echo "nohup /usr/local/bin/ssserver -c /home/***/config.json -f /tmp/ssserver.pid >> ssserver.log 2>&1 &" >> /etc/rc.local

 这样每次开机都会启动，且是后台执行。
+ client端配置   
（1）我是mac本，所以下载安装mac版的client，安装完成之后，在应用中显示图片如：   
![](/images/fq/shadowsocks.png)
（2）运行后程序会最小化在系统右上角（Windows在右下角），打开菜单，点击服务器-->>服务器设置，增加一个server，配置如下图：   
![](/images/fq/shadowconfig.png)
（3）点击确定之后，打开shadowsocks，每次服务器重启，都要重新打开一次，不然可能不会生效，操作如图：   
![](/images/fq/start.png)
（4）浏览器中打开google或者油管，看能否正常访问，  
（5）server断观察日志是否正常，如果页面能正常访问，则说明fq成功。   
（6）*`在回到server端，设置步骤（6）`*。