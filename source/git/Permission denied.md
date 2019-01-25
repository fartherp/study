# Permission denied

---

## 查看文件的权限
```
项目根路径执行
git ls-tree HEAD

结果
100644 blob 5551fde8e7dba1e37a1821e8b26374893e2a9e2e    mvnw （没有执行权限）
```

## 1.命令行添加执行权限
```
git update-index --chmod=+x gradlew

git commit -m "permission access for travis" （提交注释）

查询权限
git ls-tree HEAD

100755 blob 5551fde8e7dba1e37a1821e8b26374893e2a9e2e    mvnw
```

## 2.直接在.travis.yml 中添加命令
```
before_install:
  - chmod +x mvnw
```






