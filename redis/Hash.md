# Hash(哈希)

### hset 、hmset

```
127.0.0.1:6379> hset hash1  f1 ok ---hset key map集合一样
(integer) 1
127.0.0.1:6379> hget hash1 f1---获取一个字段值
"ok"

127.0.0.1:6379> hset hash1  f2 ok
(integer) 1
127.0.0.1:6379> hmget hash1 f1 f2----获取多个字段值
1) "ok"---f1
2) "ok"----f2

127.0.0.1:6379> hgetall hash1 ----获取全部map
1) "f1"----字段field
2) "ok"----值
3) "f2"
4) "ok"

```

### hdel

```
127.0.0.1:6379> hdel hash1 f1 --->hdel key field--->删除字段
(integer) 1
```

### hlen

```
127.0.0.1:6379> hlen hash1----->获取哈希的字段数量
(integer) 1

```

###  hkeys

```
127.0.0.1:6379> hkeys hash1--->获取所以的字段
1) "f2"
```

### hvals

$$

$$

```
127.0.0.1:6379> hvals hash1---->获取所以的值
1) "ok“
```

### Hincrby 

```
127.0.0.1:6379> hset hash1 f1 0
(integer) 1
127.0.0.1:6379> hincrby hash1 f1 1 ->hincrby key field count
(integer) 1
127.0.0.1:6379> hget hash1 f1
"1"
```

###  hsetnx

```
127.0.0.1:6379> hsetnx hash1 f1 1  
(integer) 0---->field已存在，创建不成功
```

## 应用

可以保存对象，例如：hset  user:1   name  value ，

那么string也可以保存对象，但是更多是字符串的存储