# linux的uniq

---

## testfile中的原有内容为
```
cat testfile      #原有内容  
test 30  
test 30  
test 30  
Hello 95  
Hello 95  
Hello 95  
Hello 95  
Linux 85  
Linux 85
```

## 使用uniq 命令删除重复的行后
```
uniq testfile
```

## 检查文件并删除文件中重复出现的行，并在行首显示该行重复出现的次数
```
uniq -c testfile 
```

## 当重复的行并不相邻时，uniq 命令是不起作用的，即若文件内容为以下时，uniq 命令不起作用
```
cat testfile1      # 原有内容 
test 30
Hello 95
Linux 85
test 30
Hello 95
Linux 85
test 30
Hello 95
Linux 85
```

## 排序去重
```
sort  testfile1 | uniq
```
## 统计各行在文件中出现的次数
```
sort testfile1 | uniq -c
```

## 在文件中找出重复的行
```
sort testfile1 | uniq -d
```

## 仅显示出一次的行列
```
sort testfile1 | uniq -u
```




