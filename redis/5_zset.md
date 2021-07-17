# zset

### zadd  

```
127.0.0.1:6379> zadd zset1 500 xiaohong 
(integer) 1
127.0.0.1:6379> zadd zset1 1000 jun  
(integer) 1
```

### zrangebyscore key min max

```
zrangebyscore zset1 -inf +inf --按照从小到大排序
1) "xiaohong"
2) "jun"

```

```
127.0.0.1:6379> zrangebyscore zset1 -inf 600 withscores
1) "xiaohong"      小于600降序排序
2) "500"
```

### 从大到小

```
127.0.0.1:6379> zrevrange zset1 0 -1
1) "jun"
2) "xiaohong"
```

### zrange 获取范围的值

```
127.0.0.1:6379> zrange zset1 0 -1
1) "xiaohong"
2) "jun"
```

### 获取有序集合的长度

```
127.0.0.1:6379> zcard zset1
(integer) 2
```

### 获取指定区间的数量

```
127.0.0.1:6379> zcount zset1 400 600
(integer) 1
```

## 应用

排行榜

