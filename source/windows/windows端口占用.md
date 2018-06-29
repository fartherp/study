# windows端口占用

---
## 列出所有端口的情况
```
netstat -ano
```

## 查看被占用端口对应的PID
```
netstat -aon|findstr “8081”
```

## 查看是哪个进程或者程序占用了8081端口
```
tasklist|findstr “9088”
```



