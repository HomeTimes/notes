# 起步

### 1.下载好安装包

### 2.x-ftp传到Linux中

### 3.软件解压一般解压到opt目录下

zxvf

### 4.基本环境安装

```
yum install gcc-c++

```

### 5.跳到解压redis的包下

make 命令安装

### 6.一般安装在usr/local/bin 目录下

### 7.在解压包下复制redis-conf配置文件到usr/local/bin 目录下的kconfig里

mkdir kconfig

cp   redis.conf     /usr/local/bin/kconfig

### 8.以kconfig里的配置启动redis服务

- 修改redis-conf 里的参数daemonize  为yes：表示在后台启动

- ```
  redis-server kconfig/redis.conf
  ```

  

### 9.启动redis-cli,默认端口号为6379

```
redis-cli -p  6379
```

### 10.测试是否服务开启成功

ping 

### 11.退出为：两个步奏

shutdown

exit

### 12：查看redis进程

ps -ef|grep redis

# 操作

### 1.默认有16个数据库

### 2.选择第0个数据库

select 0 

### 3.当前数据库大小

```
127.0.0.1:6379> dbsize
(integer) 1
```

### 4.插入key

```
127.0.0.1:6379> set name ok
OK
```

##### 查看key（键)

```
127.0.0.1:6379> keys *
1) "name"
2) "ni"
```

### 4.清空当前数据库

```
127.0.0.1:6379> flushdb
OK
```

```
127.0.0.1:6379> dbsize
(integer) 0
```

### 5.清空所有的数据库

```
flushall
```

### 6.五大数据类型

#### 1.String

###### 设置key-value

```
127.0.0.1:6379> set ni hoa
OK
```

###### 获取值

```
127.0.0.1:6379> get ni
"hoa"
```

###### 判断键是否存在

```
exists   键
```

###### 删除key

```
move key  db 
```

###### 查看所有的键

```
127.0.0.1:6379> keys *
1) "ni"
```

###### 设置过期时间

```
127.0.0.1:6379> EXPIRE ni 5  ni的过期时间为5秒
(integer) 1
```

还可以这样（和上面的意思一样）

```
127.0.0.1:6379> setex ni 5 hao
OK
```

###### 查看键过期的时间

```
127.0.0.1:6379> ttl ni 
(integer) 2(这是还有多少秒过期)
```

