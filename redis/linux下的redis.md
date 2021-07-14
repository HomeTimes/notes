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

- redis-server kconfig/redis.conf

### 9.启动redis-cli,默认端口号为6379

redis-cli -p  6379

### 10.测试是否服务开启成功

ping 

### 11.退出为：两个步奏

shutdown

exit

### 12：查看redis进程

ps -ef|grep redis