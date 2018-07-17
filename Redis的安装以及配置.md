<<<<<<< HEAD
[TOC]

### 一、Redis简介：

​	Redis是一个开源的使用ANSI [C语言](http://baike.baidu.com/view/1219.htm)编写、支持网络、可基于内存亦可持久化的日志型、Key-Value[数据库](http://baike.baidu.com/view/1088.htm)，并提供多种语言的API。从2010年3月15日起，Redis的开发工作由VMware主持。

​	redis是一个key-value[存储系统](http://baike.baidu.com/view/51839.htm)。和Memcached类似，它支持存储的value类型相对更多，包括string(字符串)、list([链表](http://baike.baidu.com/view/549479.htm))、set(集合)、zset(sorted set --有序集合)和hash（哈希类型）。这些[数据类型](http://baike.baidu.com/view/675645.htm)都支持push/pop、add/remove及取交集并集和差集及更丰富的操作，而且这些操作都是原子性的。在此基础上，redis支持各种不同方式的排序。与memcached一样，为了保证效率，数据都是缓存在内存中。区别的是redis会周期性的把更新的数据写入磁盘或者把修改操作写入追加的记录文件，并且在此基础上实现了master-slave(主从)同步。

### 二、安装环境：

ubantu

[Redis 2.8.13](http://download.redis.io/releases/redis-2.8.13.tar.gz)

### 三、下载安装：

##### 1.下载文件到 /opt/ 目录下

wget http://download.redis.io/releases/redis-2.8.13.tar.gz

##### 2.解归档、解压文件

```
gunzip redis-2.8.13.tar.gz

tar -xvf redis-2.8.13.tar.gz
```

##### 3.切换目录到 redis-2.8.13 目录下

```
cd redis-2.8.13
```

##### 4.执行make命令，最后几行的输出结果

```
Hint: To run 'make test' is a good idea ;)
make[1]: Leaving directory `/opt/redis-2.8.13/src'
```

##### 5.执行安装命令

```
make install
```

提示:

1. cd src && make install  
2. make[1]: Entering directory `/opt/redis-2.8.13/src'  
3.   
4. Hint: To run 'make test' is a good idea ;)  
5.   
6. ​    INSTALL install  
7. ​    INSTALL install  
8. ​    INSTALL install  
9. ​    INSTALL install  
10. ​    INSTALL install  
11. make[1]: Leaving directory `/opt/redis-2.8.13/src'  s

 根据提示，执行：cd src && make install

##### 6.修改redis配置文件

将redis.conf文件复制到/etc目录下：

```
cp  /usr/redis/redis.conf  /etc/redis/redis.conf
```

进入可视化编辑器窗口修改配置文件：

```
cd /etc/redis

vim redis.conf
```

分别修改bind、端口号，以及密码：

![](C:\Users\63458\Desktop\1111111111111\100.png)



![](C:\Users\63458\Desktop\1111111111111\101.png)



![](C:\Users\63458\Desktop\1111111111111\103.png)

### 四、如何启动redis?

​	直接到redis的安装目录下目录下执行：

```
 redis-server 
```

![img](https://img-blog.csdn.net/20141003172451656?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdGVzdGNzX2Ru/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

Server started, Redis version 2.8.13
The server is now ready to accept connections on port 6379

服务启动成功，服务已经在6379端口上监听连接请求。



### 五、如何连接redis

输入以下命令进行连接:

```
redis-cli -h 公网IP  -p  6379
```

然后输入密码：

```
auth 密码
```

测试连接是否成功，输入ping，返回pong表示redis连接成功！

### 六、遇到的问题

错误1：

![1527600777644](C:\Users\63458\AppData\Local\Temp\1527600777644.png)

解决办法：

```
cd /etc/meimei/redis.conf

vim redis.conf
```

修改bind为私网IP。（我开始写成了公网IP，导致一直出现以上错误！55555）

=======
[TOC]

### 一、Redis简介：

​	Redis是一个开源的使用ANSI [C语言](http://baike.baidu.com/view/1219.htm)编写、支持网络、可基于内存亦可持久化的日志型、Key-Value[数据库](http://baike.baidu.com/view/1088.htm)，并提供多种语言的API。从2010年3月15日起，Redis的开发工作由VMware主持。

​	redis是一个key-value[存储系统](http://baike.baidu.com/view/51839.htm)。和Memcached类似，它支持存储的value类型相对更多，包括string(字符串)、list([链表](http://baike.baidu.com/view/549479.htm))、set(集合)、zset(sorted set --有序集合)和hash（哈希类型）。这些[数据类型](http://baike.baidu.com/view/675645.htm)都支持push/pop、add/remove及取交集并集和差集及更丰富的操作，而且这些操作都是原子性的。在此基础上，redis支持各种不同方式的排序。与memcached一样，为了保证效率，数据都是缓存在内存中。区别的是redis会周期性的把更新的数据写入磁盘或者把修改操作写入追加的记录文件，并且在此基础上实现了master-slave(主从)同步。

### 二、安装环境：

ubantu

[Redis 2.8.13](http://download.redis.io/releases/redis-2.8.13.tar.gz)

### 三、下载安装：

##### 1.下载文件到 /opt/ 目录下

wget http://download.redis.io/releases/redis-2.8.13.tar.gz

##### 2.解归档、解压文件

```
gunzip redis-2.8.13.tar.gz

tar -xvf redis-2.8.13.tar.gz
```

##### 3.切换目录到 redis-2.8.13 目录下

```
cd redis-2.8.13
```

##### 4.执行make命令，最后几行的输出结果

```
Hint: To run 'make test' is a good idea ;)
make[1]: Leaving directory `/opt/redis-2.8.13/src'
```

##### 5.执行安装命令

```
make install
```

提示:

1. cd src && make install  
2. make[1]: Entering directory `/opt/redis-2.8.13/src'  
3.   
4. Hint: To run 'make test' is a good idea ;)  
5.   
6. ​    INSTALL install  
7. ​    INSTALL install  
8. ​    INSTALL install  
9. ​    INSTALL install  
10. ​    INSTALL install  
11. make[1]: Leaving directory `/opt/redis-2.8.13/src'  s

 根据提示，执行：cd src && make install

##### 6.修改redis配置文件

将redis.conf文件复制到/etc目录下：

```
cp  /usr/redis/redis.conf  /etc/redis/redis.conf
```

进入可视化编辑器窗口修改配置文件：

```
cd /etc/redis

vim redis.conf
```

分别修改bind、端口号，以及密码：

![](C:\Users\63458\Desktop\1111111111111\100.png)



![](C:\Users\63458\Desktop\1111111111111\101.png)



![](C:\Users\63458\Desktop\1111111111111\103.png)

### 四、如何启动redis?

​	直接到redis的安装目录下目录下执行：

```
 redis-server 
```

![img](https://img-blog.csdn.net/20141003172451656?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdGVzdGNzX2Ru/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

Server started, Redis version 2.8.13
The server is now ready to accept connections on port 6379

服务启动成功，服务已经在6379端口上监听连接请求。



### 五、如何连接redis

输入以下命令进行连接:

```
redis-cli -h 公网IP  -p  6379
```

然后输入密码：

```
auth 密码
```

测试连接是否成功，输入ping，返回pong表示redis连接成功！

### 六、遇到的问题

错误1：

![1527600777644](C:\Users\63458\AppData\Local\Temp\1527600777644.png)

解决办法：

```
cd /etc/meimei/redis.conf

vim redis.conf
```

修改bind为私网IP。（我开始写成了公网IP，导致一直出现以上错误！55555）

>>>>>>> 6d4205fb0fed2dc1dfdd3a97b24ef7614dc38163
![1527600868219](C:\Users\63458\AppData\Local\Temp\1527600868219.png)