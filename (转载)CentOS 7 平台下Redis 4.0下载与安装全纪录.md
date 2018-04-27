#### 1，下载
下载地址：[http://redis.io/download](http://redis.io/download)
当前最新稳定版是4.0.9，下载链接是[http://download.redis.io/releases/redis-4.0.9.tar.gz](http://download.redis.io/releases/redis-4.0.9.tar.gz)
```linux
[root@node3 ~]# wget http://download.redis.io/releases/redis-4.0.9.tar.gz
--2017-10-28 08:06:18--  http://download.redis.io/releases/redis-4.0.9.tar.gz
Resolving download.redis.io (download.redis.io)... 109.74.203.151
Connecting to download.redis.io (download.redis.io)|109.74.203.151|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1713990 (1.6M) [application/x-gzip]
Saving to: ‘redis-4.0.2.tar.gz’

100%[==============================================================================================>] 1,713,990    237KB/s   in 7.3s   

2017-10-28 08:06:26 (228 KB/s) - ‘redis-4.0.2.tar.gz’ saved [1713990/1713990]

[root@node3 ~]# 
```

#### 2,编译安装
#####（1）解压缩
```
[root@node3 ~]# tar -zxvf redis-4.0.2.tar.gz
```
#####（2）进入redis根目录
```
[root@node3 ~]# cd redis-4.0.2
```
#####（3）开始编译
```
[root@node3 redis-4.0.2]# make -j 4
cd src && make all
make[1]: Entering directory `/root/redis-4.0.2/src'
    CC Makefile.dep
make[1]: Leaving directory `/root/redis-4.0.2/src'
make[1]: Entering directory `/root/redis-4.0.2/src'
rm -rf redis-server redis-sentinel redis-cli redis-benchmark redis-check-rdb redis-check-aof *.o *.gcda *.gcno *.gcov redis.info lcov-html Makefile.dep dict-benchmark
(cd ../deps && make distclean)
make[2]: Entering directory `/root/redis-4.0.2/deps'
(cd hiredis && make clean) > /dev/null || true
(cd linenoise && make clean) > /dev/null || true
(cd lua && make clean) > /dev/null || true
(cd jemalloc && [ -f Makefile ] && make distclean) > /dev/null || true
(rm -f .make-*)
make[2]: Leaving directory `/root/redis-4.0.2/deps'
(rm -f .make-*)
echo STD=-std=c99 -pedantic -DREDIS_STATIC='' >> .make-settings
echo WARN=-Wall -W -Wno-missing-field-initializers >> .make-settings
echo OPT=-O2 >> .make-settings
echo MALLOC=jemalloc >> .make-settings
echo CFLAGS= >> .make-settings
echo LDFLAGS= >> .make-settings
echo REDIS_CFLAGS= >> .make-settings
echo REDIS_LDFLAGS= >> .make-settings
echo PREV_FINAL_CFLAGS=-std=c99 -pedantic -DREDIS_STATIC='' -Wall -W -Wno-missing-field-initializers -O2 -g -ggdb   -I../deps/hiredis -I../deps/linenoise -I../deps/lua/src -DUSE_JEMALLOC -I../deps/jemalloc/include >> .make-settings
echo PREV_FINAL_LDFLAGS=  -g -ggdb -rdynamic >> .make-settings
(cd ../deps && make hiredis linenoise lua jemalloc)
make[2]: Entering directory `/root/redis-4.0.2/deps'
(cd hiredis && make clean) > /dev/null || true
(cd linenoise && make clean) > /dev/null || true
(cd lua && make clean) > /dev/null || true
(cd jemalloc && [ -f Makefile ] && make distclean) > /dev/null || true
(rm -f .make-*)
(echo "" > .make-cflags)
(echo "" > .make-ldflags)
MAKE hiredis
cd hiredis && make static
MAKE linenoise
cd linenoise && make
make[3]: Entering directory `/root/redis-4.0.2/deps/linenoise'
cc  -Wall -Os -g  -c linenoise.c
MAKE lua
cd lua/src && make all CFLAGS="-O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC='' " MYLDFLAGS="" AR="ar rcu"
make[3]: cc: Command not found
make[3]: *** [linenoise.o] Error 127
make[3]: Leaving directory `/root/redis-4.0.2/deps/linenoise'
make[2]: *** [linenoise] Error 2
make[2]: *** Waiting for unfinished jobs....
make[3]: Entering directory `/root/redis-4.0.2/deps/hiredis'
gcc -std=c99 -pedantic -c -O3 -fPIC  -Wall -W -Wstrict-prototypes -Wwrite-strings -g -ggdb  net.c
make[3]: Entering directory `/root/redis-4.0.2/deps/lua/src'
cc -O2 -Wall -DLUA_ANSI -DENABLE_CJSON_GLOBAL -DREDIS_STATIC=''    -c -o lapi.o lapi.c
make[3]: gcc: Command not found
make[3]: *** [net.o] Error 127
make[3]: Leaving directory `/root/redis-4.0.2/deps/hiredis'
make[2]: *** [hiredis] Error 2
make[3]: cc: Command not found
make[3]: *** [lapi.o] Error 127
make[3]: Leaving directory `/root/redis-4.0.2/deps/lua/src'
make[2]: *** [lua] Error 2
make[2]: Leaving directory `/root/redis-4.0.2/deps'
make[1]: [persist-settings] Error 2 (ignored)
    CC adlist.o
/bin/sh: cc: command not found
    CC quicklist.o
make[1]: *** [adlist.o] Error 127
make[1]: *** Waiting for unfinished jobs....
/bin/sh: cc: command not found
make[1]: *** [quicklist.o] Error 127
make[1]: Leaving directory `/root/redis-4.0.2/src'
make: *** [all] Error 2
[root@node3 redis-4.0.2]
```
#####（4）解决依赖关系 
 由于新安装的Linux系统没有安装gcc环境
 ```
 [root@node3 redis-4.0.2]# yum install -y gcc
 ```
 ```
 [root@node3 redis-4.0.2]# make -j 4
cd src && make all
make[1]: Entering directory `/root/redis-4.0.2/src'
    CC Makefile.dep
make[1]: Leaving directory `/root/redis-4.0.2/src'
make[1]: Entering directory `/root/redis-4.0.2/src'
    CC adlist.o
    CC quicklist.o
    CC ae.o
    CC anet.o
In file included from adlist.c:34:0:
zmalloc.h:50:31: fatal error: jemalloc/jemalloc.h: No such file or directory
 #include <jemalloc/jemalloc.h>
                               ^
compilation terminated.
In file included from quicklist.c:33:0:
zmalloc.h:50:31: fatal error: jemalloc/jemalloc.h: No such file or directory
 #include <jemalloc/jemalloc.h>
                               ^
compilation terminated.
In file included from ae.c:44:0:
zmalloc.h:50:31: fatal error: jemalloc/jemalloc.h: No such file or directory
 #include <jemalloc/jemalloc.h>
                               ^
compilation terminated.
make[1]: *** [adlist.o] Error 1
make[1]: *** Waiting for unfinished jobs....
make[1]: *** [quicklist.o] Error 1
make[1]: *** [ae.o] Error 1
make[1]: Leaving directory `/root/redis-4.0.2/src'
make: *** [all] Error 2
[root@node3 redis-4.0.2]# 
 ```
 ```
 [root@node3 redis-4.0.2]# yum install -y jemalloc-devel
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirrors.aliyun.com
 * extras: mirrors.aliyun.com
 * updates: mirrors.aliyun.com
No package jemalloc-devel available.
Error: Nothing to do
[root@node3 redis-4.0.2]#
 ```
 百度一下，有网友说可以这样解决make MALLOC=libc，下面试试
 ```
 [root@node3 redis-4.0.2]# make -j 4 MALLOC=libc
....

Hint: It's a good idea to run 'make test' ;)

make[1]: Leaving directory `/root/redis-4.0.2/src'
[root@node3 redis-4.0.2]# 
 ```
 编译完成。
 ```
 [root@node3 redis-4.0.2]# make test
cd src && make test
make[1]: Entering directory `/root/redis-4.0.2/src'
You need tcl 8.5 or newer in order to run the Redis test
make[1]: *** [test] Error 1
make[1]: Leaving directory `/root/redis-4.0.2/src'
make: *** [test] Error 2
[root@node3 redis-4.0.2]#
 ```
 提示需要安装tcl 
 ```
 [root@node3 redis-4.0.2]# yum install -y tcl
 ```
 再次测试
 ```
 [root@node3 redis-4.0.2]# make test
...

  167 seconds - unit/obuf-limits

\o/ All tests passed without errors!

Cleanup: may take some time... OK
make[1]: Leaving directory `/root/redis-4.0.2/src'
[root@node3 redis-4.0.2]# 
 ```
 最终编译完成。
 #### 编译总结：

- 编译前需要安装依赖 yum install -y gcc tcl
- 然后再编译 make -j 4 MALLOC=libc
```
[root@node3 redis-4.0.2]# make install
cd src && make install
make[1]: Entering directory `/root/redis-4.0.2/src'

Hint: It's a good idea to run 'make test' ;)

    INSTALL install
    INSTALL install
    INSTALL install
    INSTALL install
    INSTALL install
make[1]: Leaving directory `/root/redis-4.0.2/src'
[root@node3 redis-4.0.2]# 
```
#### 3、配置
Redis外部访问
```
[root@node3 redis-4.0.2]# vi redis.conf
```
修改3处：
- 注释掉 #bind 127.0.0.1
- 设置守护进程 daemonize yes
- 禁用保护模式 protected-mode no
#### 4、启动服务
编译后，在src目录下将出现一个redis服务程序redis-server  
使用下面命令启动，通过启动参数告诉redis使用指定配置文件
```
[root@node3 redis-4.0.2]# src/redis-server redis.conf 
7311:C 28 Oct 08:49:25.126 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
7311:C 28 Oct 08:49:25.126 # Redis version=4.0.2, bits=64, commit=00000000, modified=0, pid=7311, just started
7311:C 28 Oct 08:49:25.126 # Configuration loaded
[root@node3 redis-4.0.2]# ps -aux|grep redis
root       7312  0.0  0.1 141768  1964 ?        Ssl  08:49   0:00 src/redis-server *:6379
root       7317  0.0  0.0 112660   964 pts/0    S+   08:49   0:00 grep --color=auto redis
[root@node3 redis-4.0.2]# 
```
#### 5、使用redis-cli访问redis
```
[root@node3 redis-4.0.2]# src/redis-cli 
127.0.0.1:6379> set "hadron" "chengyuqiang"
OK
127.0.0.1:6379> get "hadron"
"chengyuqiang"
127.0.0.1:6379> 
```