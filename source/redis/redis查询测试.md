# redis查询测试

---
## SortedSet
```
id time
```

## pair条件数据
```
ZADD {cyq}-pair 1528128000 1
ZADD {cyq}-pair 1528041600 2
ZADD {cyq}-pair 1527955200 3
```

## type条件数据
```
ZADD {cyq}-type 1527955200 3
ZADD {cyq}-type 1528214400 4
ZADD {cyq}-type 1528128000 1
```

## or条件
```
ZUNIONSTORE {cyq}-salary-or 2 {cyq}-pair {cyq}-type AGGREGATE MIN
```

## and条件
```
ZINTERSTORE {cyq}-salary-and 2 {cyq}-pair {cyq}-type AGGREGATE MIN
```

## 查询数量（总数）
```
ZCOUNT {cyq}-salary-or 1528041600 1528128000 
```

## 倒叙查询获取id（start：开始条数，stop：结束条数）
```
ZREVRANGE {cyq}-salary-and 0 2 WITHSCORES
```

## 通过id查询具体数据
```
HGET key-1
HGET key-2
```

## 根据时间戳倒叙查询
```
ZREVRANGEBYSCORE {cyq}-salary-or 1528128000 1528041600 WITHSCORES
```



