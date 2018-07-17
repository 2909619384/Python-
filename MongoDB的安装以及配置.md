# MongoDB的安装以及配置

​	MongoDB是一个NoSQL数据库。它是使用C++编写的开源、跨平台，面向文档的数据库。

##### 1.在mongDB官网下载mongoDB

```
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.6.5.tgz 
```

##### 2.解归档

```
gunzip <filename>
```

##### 3.解压缩

```
tar -xvf <filename>
```

##### 4.将mongodb文件移动到/usr/local/<source>文件夹下

```
mv <source>  /usr/local/<source>
```

##### 5.进入用户主目录

```
cd ~
```

##### 6.进入.bashrc,添加环境变量信息

```
vim .bashrc
```

```
PATH=$PATH:/usr/local/mongo-3.6.5/bin

export PATH
```

注意：以上为ubuntu配置，如果是centerOS系统，进入vim .bash_profile文件添加环境变量信息，PATH=.....:/usr/local/<source>/bin

##### 7.保存以上配置后退出，检查环境变量是否配置成功

```
echo $PATH
```

##### 8.启动mongo,当输出如下信息表示配置成功

![](C:\Users\63458\Desktop\1111111111111\41.png)

##### 9.绑定私有IP和端口

```
mongod --bind_ip 私有IP  --port 27017 --quiet
```

##### 10.绑定公网IP和端口

```
mongo --host 公网IP --port 27017
```

当输出如下信息表示启动成功：

![](C:\Users\63458\Desktop\1111111111111\42.png)

##### 11.遇到的问题

运行mongo --host 公网IP --port 27017连接失败，解决办法：

```
netstat -anp|grep  mongo  #查看mongo的端口是否被占用

ps -ef|grep mongod    #查看mongo的端口

kill -9 PID   #强杀进程
```

然后运行：

```
mongod --bind_ip 私有IP --port 27017 --quiet
```

重新启动一个命令窗口运行：

```
mongo --host 公网IP  --port 27017
```

注意：我的主要问题是，每次运行mongod --bind_ip 私有IP --port 27017 --quiet后，我会直接在同一个命令窗口运行mongo --host 公网IP  --port 27017，这样导致一直连接不上。应该再重新开一个命令窗口运行命令。

