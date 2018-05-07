### 1，ls -l  
查看当前目录下所有可见文件
### 2，sudo
sudo是linux系统管理指令，是允许系统管理员让普通用户执行一些或者全部的root命令的一个工具
### 3，/etc/profile
系统整体设置
### 4，sudo vi .bash_profile
用户个人变量  
### 5，根据用户个人变量更新jdk 步骤
sudo vi .bash_profile  
按i  
左下角有个insert  
上下左右建 移动光标  
改完后 按esc  
：wq   保存退出  
：q   是退出 不保存  
：q！强制退出  
source .bash_profile 

### 6，端口查看
1、lsof -i:端口号
2、netstat -tunlp|grep 端口号
都可以查看指定端口被哪个进程占用的情况
[参考](https://www.cnblogs.com/CEO-H/p/7794306.html)
### 7,查看磁盘空间大小命令
```
df -hl 查看磁盘剩余空间
df -h 查看每个根路径的分区大小
du -sh [目录名] 返回该目录的大小
du -sm [文件夹] 返回该文件夹总M数
du -h [目录名] 查看指定文件夹下的所有文件大小（包含子文件夹）
```
```
查看硬盘的分区 #sudo fdisk -l
　　查看IDE硬盘信息 #sudo hdparm -i /dev/hda=
　　查看STAT硬盘信息 #sudo hdparm -I /dev/sda 或 #sudo apt-get install blktool #sudo blktool/dev/sda id
　　查看硬盘剩余空间 #df -h #df -H
　　查看目录占用空间 #du -hs 目录名
　　优盘没法卸载 #sync fuser -km /media/usbdisk
```

### 8，文件夹
##### 1，创建文件夹 sudo mkdir data
##### 2，拷贝文件夹 sudo cp src/redis-server src/redis-cli src/redis-benchmark src/redis-check-aof src/redis-sentinel src/redis-check-rdb /usr/local/redis/bin/
##### 3,sudo ls -l /usr/local/redis/etc/

### 9,linux查看防火墙状态及开启关闭命令
一、service方式

查看防火墙状态：

[root@centos6 ~]# service iptables status

iptables：未运行防火墙。

开启防火墙：

[root@centos6 ~]# service iptables start

关闭防火墙：

[root@centos6 ~]# service iptables stop
二、iptables方式

先进入init.d目录，命令如下：

[root@centos6 ~]# cd /etc/init.d/

[root@centos6 init.d]#

然后

查看防火墙状态：

[root@centos6 init.d]# /etc/init.d/iptables status

暂时关闭防火墙：

[root@centos6 init.d]# /etc/init.d/iptables stop

重启iptables：

[root@centos6 init.d]# /etc/init.d/iptables restart

### 10,linux如何查看端口被哪个进程占用？[参考](https://www.cnblogs.com/CEO-H/p/7794306.html)
1、lsof -i:端口号

2、netstat -tunlp|grep 端口号

都可以查看指定端口被哪个进程占用的情况

3、杀死端口
lsof -i:8082  
```
java    4638 root   41u  IPv6  23412      0t0  TCP *:us-cli (LISTEN)
```
kill -9 4638

4,输入netstat -tln,查看系统当前所有被占用端口,主要是为了查看你的端口是否真正的被占用着,搭建可以看到我的9001,和9002端口都已经被占用了,所以我需要释放这两个端口
