# mongodb日期查询
## 日期
```
db.getCollection('test').find({"time":{$gte:ISODate("2019-06-01T00:00:00.303Z"), $lte:ISODate("2019-11-30T00:00:00.303Z")}})
```