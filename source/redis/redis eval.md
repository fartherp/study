# redis eval

---
## 设置k-v，设置有效期
```
redis.call('set', KEYS[1], ARGV[1]) redis.call('expire', KEYS[1], ARGV[2])
```

## incrby，设置过期时间，返回自增值
```
local value = redis.call('incrby', KEYS[1], ARGV[1]) redis.call('expire', KEYS[1], ARGV[2]) return value
```

## 每日累计次数，1返回成功，0返回失败
```
eval "local key = KEYS[1] 
local redis_key = KEYS[2] 
local filed = ARGV[1] 
local value = ARGV[2] 
local jsonString = redis.call('hget',key,filed) 
local json = cjson.decode(jsonString) 
local redis_value = redis.call('get', redis_key) 
if redis_value==false then redis_value = 0 end 
local sum = tonumber(redis_value) + tonumber(value) 
if (tonumber(sum) <= tonumber(json[ARGV[3]])) then redis.call('set', redis_key, tonumber(sum)) return 1 else return 0 end " 2 {cyq}.tableName {cyq}.maxcount trade.*.*.* 1 maxCount
```




