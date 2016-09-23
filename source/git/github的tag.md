# github的tag

---

##查看
###列出所有
```
git tag
```
###列出按字母排序
```
只列出1.*的版本
git tag -l v1.*
和创建时间没关系
```
###提交信息
```
git log --oneline
```

##创建
###轻量级
```
git tag v1.0
```
###注释
```
git tag -a v1.0 -m 'first version'
-m: 注释信息
```
###签名
```
git tag -s v1.0 8atcbc2
```

##删除
```
git tag -d v1.0
```

##验证
```
git tag -v v1.0
```

##共享/发布
```
git push origin --tags
```





