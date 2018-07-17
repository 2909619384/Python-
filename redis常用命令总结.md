<<<<<<< HEAD
# redis常用命令

##### 1.连接redis

```
redis -cli -h 公网IP -p 6379
```

##### 2.验证用户信息

```
auth password
```

##### 3.插入数据

```
rpush foo 1 2 3 4 5 
```

##### 4.移除并返回列表key的头元素

```
lpop foo
```

##### 5.查询所有符合给定模式pattern的key

```
keys  *
```

#####  6.判断member元素是否集合key中成员

```
member key名
```

##### 7.清除数据库

```
flushdb
```



更多命令参考教程：http://doc.redisfans.com/

=======
# redis常用命令

##### 1.连接redis

```
redis -cli -h 公网IP -p 6379
```

##### 2.验证用户信息

```
auth password
```

##### 3.插入数据

```
rpush foo 1 2 3 4 5 
```

##### 4.移除并返回列表key的头元素

```
lpop foo
```

##### 5.查询所有符合给定模式pattern的key

```
keys  *
```

#####  6.判断member元素是否集合key中成员

```
member key名
```

##### 7.清除数据库

```
flushdb
```



更多命令参考教程：http://doc.redisfans.com/

>>>>>>> 6d4205fb0fed2dc1dfdd3a97b24ef7614dc38163
