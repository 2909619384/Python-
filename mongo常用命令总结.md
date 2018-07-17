# mongo常用命令总结

##### 1.连接mongo

```
mongod  --bind_ip  私有IP --port 27017 --quiet

mongo --host  公有IP --port 27017
```

##### 2.查看当前所在的数据库

```
db
```

##### 3.显示所有数据库

```
show dbs
```

##### 4.切换数据库

```
use test
```

##### 5.创建表

```
db.createCollections('表名')
```

##### 6.想查看test数据库中有哪些表

```
show collections
```



