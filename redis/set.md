# set（集合）

说明：无序，不重复的集合

### 1.设置值

```
127.0.0.1:6379> sadd set1 ok
(integer) 1
```

### 2.获取值

```
127.0.0.1:6379> smembers set1
1) "ok"
```

### 3.包含

```
127.0.0.1:6379> smembers set1
1) "ok"
127.0.0.1:6379> sismember set1 ll     #判断某个值是否在set集合
(integer) 0
```

### 4.长度

```
127.0.0.1:6379> scard set1
(integer) 1         --------------》长度

```

### 5.删除指定元素

```
127.0.0.1:6379> smembers set1
1) "ok1"
2) "ok"
127.0.0.1:6379> srem set1 ok---->srem key member
(integer) 1
127.0.0.1:6379> smembers set1
1) "ok1"
```

### 6.随机获取元素

```
127.0.0.1:6379> srandmember set1 ----------》 srandmember key 【count】
"ok1"
127.0.0.1:6379> srandmember set1 2
1) "lp"
2) "ok1"

```

### 7.随机移除元素

```
127.0.0.1:6379> spop set1
"ok1"
```

### 8.并集、交集(类似微博、bili共同关注)、差集

```
127.0.0.1:6379> sadd set1 a
(integer) 1
127.0.0.1:6379> sadd set1 a
(integer) 0
127.0.0.1:6379> sadd set1 b
(integer) 1
127.0.0.1:6379> sadd set2 a
(integer) 1
127.0.0.1:6379> sadd set2 c
(integer) 1
127.0.0.1:6379> sdiff set1 set2 -->set1(主)和set2的差集
1) "b"
127.0.0.1:6379> sinter set1 set2--->交集
1) "a"
127.0.0.1:6379> sunion set1 set2-->并集
1) "c"
2) "b"
3) "a"
```

