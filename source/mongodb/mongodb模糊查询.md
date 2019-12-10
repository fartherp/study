# mongodb模糊查询
## 使用RockMongo客户端工具进行模糊查询
```
{"content":"$regex": "123456"}
```
## 查询包含XXX
```
db.getCollection('test').find({name:/xxx/})
```
## 查询以XXX开头
```
db.getCollection('test').find({name:/^xxx/})
```
## 查询以XXX结尾
```
db.getCollection('test').find({name:/xxx^/})
```
## 查询忽略大小写
```
db.getCollection('test').find({name:/xxx/i})
```
## Spring中不区分大小写的模糊查询
```
//完全匹配
Pattern pattern = Pattern.compile("^王$", Pattern.CASE_INSENSITIVE);
//右匹配
Pattern pattern = Pattern.compile("^.*王$", Pattern.CASE_INSENSITIVE);
//左匹配
Pattern pattern = Pattern.compile("^王.*$", Pattern.CASE_INSENSITIVE);
//模糊匹配
Pattern pattern = Pattern.compile("^.*王.*$", Pattern.CASE_INSENSITIVE);
Query query = Query.query(Criteria.where(fieldName).regex(pattern)); 
List<simpleuserinfo> users = mongoTemplate.find(query, SimpleUserInfo.class, classname);
return users;
```