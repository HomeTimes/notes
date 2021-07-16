### List列表

###### 把列表玩成了栈、队列、

```
127.0.0.1:6379> lpush list1 one two three(lpush key elemnts )
(integer) 3
127.0.0.1:6379> get list1( 不是get获取)
(error) WRONGTYPE Operation against a key holding the wrong kind of value
127.0.0.1:6379> lrange list1 0 -1 (获取列表)
1) "three"
2) "two"
3) "one" -------------------先进后出
```

###### rpush也可以从右边进入列表

```
127.0.0.1:6379> rpush list1 forth (向右如列表)
(integer) 4
127.0.0.1:6379> lrange list1 0 -1  (获取列表的数据)
1) "three"
2) "two"
3) "one"
4) "forth"

```

###### rpop从右边出列表

```
127.0.0.1:6379> rpop list1
"forth"
```

也可以左边

###### lindex通过下标获取列表的元素

```
127.0.0.1:6379> lindex list1 0
"three"
```

###### llen返回列表的长度

```
127.0.0.1:6379> llen list1
(integer) 3
```

###### 移除lrem指定个数的值

 lrem  key  count  value：精确匹配

```
27.0.0.1:6379> lrange list1 0 -1
1) "three"
2) "two"
3) "one"
127.0.0.1:6379> lrem list1 1 one 
(integer) 1
127.0.0.1:6379> lrange list1 0 -1
1) "three"
2) "two"
```

###### ltrim截取列表

```
127.0.0.1:6379> lrange list1 0 -1  (截取list列表里某范围的值，list的值也被改变)
1) "three"
2) "two"
127.0.0.1:6379> ltrim list1 0  0
OK
127.0.0.1:6379> lrange list1 0 -1
1) "three"

```

###### rpoplpush（组合命令）

```
127.0.0.1:6379> lrange list1 0 -1
1) "three"
127.0.0.1:6379> rpoplpush list1  list2 (从list1列表pop移除元素push到list2中)
"three"
127.0.0.1:6379> lrange list2 0 -1
1) "three"
```

###### 更新列表下标的值

```
127.0.0.1:6379> exists list (判断这个列表是否存在)
(integer) 0
127.0.0.1:6379> lset list 0 mmm
(error) ERR no such key (列表（key）不存在，设置下标(更新)值，会报错)
127.0.0.1:6379> lpush list1 mmm
(integer) 1
127.0.0.1:6379> lrange list1 0 -1
1) "mmm"
127.0.0.1:6379> lset list1 0  ok
OK
127.0.0.1:6379> lrange list1 0 0
1) "ok"
```

###### 将某个具体的值插入指定值得后面（前面）

```
127.0.0.1:6379> lrange list1 0  -1
1) "ok1"
2) "ok"
127.0.0.1:6379> linsert list1 after ok1 ok0 (在ok1的后面插入值)
(integer) 3
127.0.0.1:6379> lrange list1  0 -1 
1) "ok1"
2) "ok0"
3) "ok"
```

小结：

- 像是链表：插入指定（不指定）值得后面（前面）

```
rpush 、lpush
```

- 链表不存在，创建新的链表

- 如果链表存在，
- 移除了所有元素，也意味者空链表，链表不存在

```
127.0.0.1:6379> rpop  list1
"ok"
127.0.0.1:6379> rpop  list1
"ok0"
127.0.0.1:6379> rpop  list1
"ok1"
127.0.0.1:6379> exists list1
(integer) 0

```

- 在两边插入或该动值，效率最高，中间元素，相对来说效率会低一些

###### 思考

- （Lpush   Lpop）从左边进去，从左边拿,这是(栈)：先进后出
- （Lpush  rpop） 从左边进去，从右边拿，这是消息队列