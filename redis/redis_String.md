#### 1.String

###### 设置key-value

```
127.0.0.1:6379> set ni hoa
OK
setnx key value(key不存在就创建成功，否则创建失败)
```

###### 获取值

```
127.0.0.1:6379> get ni
"hoa"
```

###### 判断键的类型

```
type key
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
127.0.0.1:6379> ttl key 
(integer) 2(这是还有多少秒过期)
```

###### 值追加

```
127.0.0.1:6379> keys *
1) "ni"
127.0.0.1:6379> get ni
"hao"
127.0.0.1:6379> append ni la  (如果key不存在，就set 一个key)
(integer) 5
127.0.0.1:6379> get ni
"haola"
```

###### 看key的长度

```
127.0.0.1:6379> strlen ni
(integer) 5
```

###### 自增+1

```
127.0.0.1:6379> set ok 0
OK
127.0.0.1:6379> incr ok -------自增+1
(integer) 1
127.0.0.1:6379> get ok
"1"
```

###### 自增+N

```
127.0.0.1:6379> incrby ok 5
(integer) 7
127.0.0.1:6379> get ok
"7"
```

###### 自-1

```
127.0.0.1:6379> decr ok
(integer) 6
127.0.0.1:6379> get ok
"6"
```

###### 自-N

```
127.0.0.1:6379> decrby ok 2
(integer) 4
127.0.0.1:6379> get ok
"4"
```

###### 获得指定字符串长度范围的 值

```
127.0.0.1:6379> getRange ni 0 3
"haol"
127.0.0.1:6379> getrange ni 0 -1
"haola"
```

###### 指定开始的字符串setrange key offset value

```
127.0.0.1:6379> getrange ni 0 -1
"haola"
127.0.0.1:6379> setrange ni 1 kk
(integer) 5
127.0.0.1:6379> get ni
"hkkla"
```

就是从下表开始的地方开始替换

###### 批量设置key-value

```
mset key1 vlaue key2 value .......
```

```
msetnx k1 v1 k2 v2  (这是个原子性的操作，要么成功要么失败)
```

###### 批量获取

```
mget key1 key2.......
```

```

```

###### 先get后set

```
127.0.0.1:6379> getset ol mu  （如果不存在，返回nil，再set key）
(nil)
127.0.0.1:6379> get ol
"mu"
127.0.0.1:6379> getset ol kk
"mu"
127.0.0.1:6379> get ol
"kk"

```

#### String进价

##### 对象的思想

###### set  user：1{name :www,age:10}：用户1的信息

```
127.0.0.1:6379> mset user:1:name www  user:1:age 10
OK
127.0.0.1:6379> keys *
1) "user:1:name"
2) "user:1:age"
127.0.0.1:6379> mget user:1:name user:1:age 
1) "www"
2) "10"
```

###### 还可以设置为文章的点击数