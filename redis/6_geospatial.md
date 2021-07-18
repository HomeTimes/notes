# 地理空间位置

### geoadd添加地理位置

```
127.0.0.1:6379> geoadd china:city 116.352963  40.409079  beijing
(integer) 1
```

### geopos返回位置

```
127.0.0.1:6379> geopos china:city beijing
1) 1) "116.35296374559402466"
   2) "40.40907855875487797"
```

### geodist计算两地的距离

没有显式的使用单位，那么默认单位是米，geodist命令在计算距离时会假设地球为完美的球形， 在极限情况下， 这一假设最大会造成 0.5% 的误差。

```
127.0.0.1:6379> geodist china:city beijing guangzhou
"55830.8909"-----单位为
```

### georedius

应用：找指定范围内的人

```
georadius china:city 110 30 5000 km  
1) "guangzhou"          以110,30为中心，找出半径为5000km范围的城市
2) "beijing"
```

```
georadius china:city 110 30 5000 km  withcoord --显示他人的定位信息
1) 1) "guangzhou"
   2) 1) "116.41338318586349487"
      2) "39.9092492891813535"
2) 1) "beijing"
   2) 1) "116.35296374559402466"
      2) "40.40907855875487797"

```

```
127.0.0.1:6379> georadius china:city 110 30 5000 km withdist
1) 1) "guangzhou" ---显示到中心的距离
   2) "1246.7463"
2) 1) "beijing"
   2) "1292.8165"
```

```
127.0.0.1:6379> georadius china:city 110 30 5000 km withcoord count 1
1) 1) "guangzhou"
   2) 1) "116.41338318586349487"
      2) "39.9092492891813535"
127.0.0.1:6379> georadius china:city 110 30 5000 km withcoord count 2
1) 1) "guangzhou"
   2) 1) "116.41338318586349487"
      2) "39.9092492891813535"
2) 1) "beijing"
   2) 1) "116.35296374559402466"
      2) "40.40907855875487797"  ---筛选出指定的结果
```

### georadiusbymember

##找出指定元素周围的其他元素

```
127.0.0.1:6379> georadiusbymember china:city beijing 10000 km  ---在北京10000km以内的城市
1) "guangzhou"
2) "beijing"
```

### geohash 

##将二维的经纬度转换为一维的字符串，如果两个字符串越接近，那么则距离越近

```
127.0.0.1:6379> geohash china:city beijing guangzhou
1) "wx4tzsjxuw0"
2) "wx4g1138hr0"
```

geo底层的实现原理都是zset

```
127.0.0.1:6379> zrange china:city 0 -1 --查看所有的元素
1) "guangzhou"
2) "beijing"
```

移除元素

```
zrem key field
```

