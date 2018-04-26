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
