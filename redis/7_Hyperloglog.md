# HyperLoglog

### 应用

网页的的uv(一个人访问一个网站多次，但是还是算作一个人)

### 传统的方式：

set集合保存用户的id，然后就可以统计set中的元素数量作为标准判断

### 优点：

用hyperloglog，占用的内存是固定的，2^64不同的元素的技术，只需要费12kb的的内存，如果要从内存角度来比较的话Hyperloglog首选

容错率:0.81%,可以忽略不计

### 测试

```
127.0.0.1:6379> pfadd mykey  a b c ---添加元素
(integer) 1
127.0.0.1:6379> pfcount mykey ---元素的个数(元素不重复)
(integer) 3  ----个数
127.0.0.1:6379> pfadd mykey1 a b c d d e
(integer) 1 
127.0.0.1:6379> pfcount mykey1 
(integer) 5 ----个数
127.0.0.1:6379> pfmerge mykey2 mykey mykey1
OK  -----两个合并成一个新的mykey2
127.0.0.1:6379> pfcount mykey2
(integer) 5 ----统计各少数
```

