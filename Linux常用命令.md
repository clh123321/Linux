#### 1，ls -l  
查看当前目录下所有可见文件
#### 2，sudo
sudo是linux系统管理指令，是允许系统管理员让普通用户执行一些或者全部的root命令的一个工具
#### 3，/etc/profile
系统整体设置
#### 4，sudo vi .bash_profile
用户个人变量  
#### 5，根据用户个人变量更新jdk 步骤
sudo vi .bash_profile  
按i  
左下角有个insert  
上下左右建 移动光标  
改完后 按esc  
：wq   保存退出  
：q   是退出 不保存  
：q！强制退出  
source .bash_profile 

#### 6，端口查看
1、lsof -i:端口号
2、netstat -tunlp|grep 端口号
都可以查看指定端口被哪个进程占用的情况
[参考](https://www.cnblogs.com/CEO-H/p/7794306.html)
#### 7,查看磁盘空间大小命令
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