# linux的awk

---

## 显示最近登录的5个帐号信息
```
last -n 5
```

## 只是显示最近登录的5个帐号
```
last -n 5 | awk  '{print $1}'
awk工作流程是这样的：读入有'\n'换行符分割的一条记录，然后将记录按指定的域分隔符划分域，填充域，$0则表示所有域,$1表示第一个域,$n表示第n个域。默认域分隔符是"空白键" 或 "[tab]键",所以$1表示登录用户，$3表示登录用户ip,以此类推。
```

## 只是显示/etc/passwd的账户
```
cat /etc/passwd |awk  -F ':'  '{print $1}'  
```

## 只是显示/etc/passwd的账户和账户对应的shell,而账户与shell之间以tab键分割
```
cat /etc/passwd |awk  -F ':'  '{print $1"\t"$7}'
```

## 只是显示/etc/passwd的账户和账户对应的shell,而账户与shell之间以逗号分割,而且在所有行添加列名name,shell,在最后一行添加"blue,/bin/nosh"
```
cat /etc/passwd |awk  -F ':'  'BEGIN {print "name,shell"}  {print $1","$7} END {print "blue,/bin/nosh"}'
awk工作流程是这样的：先执行BEGING，然后读取文件，读入有/n换行符分割的一条记录，然后将记录按指定的域分隔符划分域，填充域，$0则表示所有域,$1表示第一个域,$n表示第n个域,随后开始执行模式所对应的动作action。接着开始读入第二条记录······直到所有的记录都读完，最后执行END操作。
```
## 搜索/etc/passwd有root关键字的所有行
```
awk -F: '/root/' /etc/passwd
这种是pattern的使用示例，匹配了pattern(这里是root)的行才会执行action(没有指定action，默认输出每行的内容)。
搜索支持正则，例如找root开头的: awk -F: '/^root/' /etc/passwd
```

## 搜索/etc/passwd有root关键字的所有行，并显示对应的shell
```
awk -F: '/root/{print $7}' /etc/passwd 
这里指定了action{print $7}
```

## awk内置变量
```
ARGC               命令行参数个数
ARGV               命令行参数排列
ENVIRON            支持队列中系统环境变量的使用
FILENAME           awk浏览的文件名
FNR                浏览文件的记录数
FS                 设置输入域分隔符，等价于命令行 -F选项
NF                 浏览记录的域的个数
NR                 已读的记录数
OFS                输出域分隔符
ORS                输出记录分隔符
RS                 控制记录分隔符
```

## 统计/etc/passwd:文件名，每行的行号，每行的列数，对应的完整行内容:
```
awk  -F ':'  '{print "filename:" FILENAME ",linenumber:" NR ",columns:" NF ",linecontent:"$0}' /etc/passwd
```




