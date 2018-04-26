## 1，安装telnet
#### 1，检测telnet-server的rpm包是否安装  
[root@localhost ~]# rpm -qa telnet-server  
若无输入内容，则表示没有安装。出于安全考虑telnet-server.rpm是默认没有安装的，而telnet的客户端是标配。即下面的软件是默认安装的。
#### 2，若未安装，则安装telnet-server，否则忽略此步骤
[root@localhost ~]#yum install telnet-server 　
#### 3，检测telnet-server的rpm包是否安装
[root@localhost ~]# rpm -qa telnet  
telnet-0.17-47.el6_3.1.x86_64
#### 4，若未安装，则安装telnet，否则忽略此步骤
[root@localhost ~]# yum install telnet

## 2，重新启动xinetd守护进程 
由于telnet服务也是由xinetd守护的，所以安装完telnet-server，要启动telnet服务就必须重新启动xinetd  
[root@locahost ~]#service xinetd restart 
## 3，测试
我们先来查看TCP的23端口是否开启正常  
[root@localhost ~]#netstat -tnl |grep 23  
tcp 0 0 0.0.0.0:23 0.0.0.0:* LISTEN  
如果上面的一行存在就说明服务已经运行了。如果netstat命令没有返回内容，我们就只好继续进行更深入的配置了。