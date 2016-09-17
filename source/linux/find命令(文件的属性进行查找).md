# find命令（文件的属性进行查找）

---

##按照文件名查找
###在根目录下查找文件httpd.conf，表示在整个硬盘查找
```
find / -name httpd.conf
```
###在/etc目录下文件httpd.conf
```
find /etc -name httpd.conf
```
###使用通配符*(0或者任意多个)。表示在/etc目录下查找文件名中含有字符串‘srm’的文件
```
find /etc -name '*srm*'
```
###表示当前目录下查找文件名开头是字符串‘srm’的文件
```
find . -name 'srm*'
```
##按照文件特征查找
###查找在系统中最后10分钟访问的文件
```
find / -amin -10
```
###查找在系统中最后48小时访问的文件
```
find / -atime -2
```
###查找在系统中为空的文件或者文件夹
```
find / -empty
```
###查找在系统中属于 group为cat的文件
```
find / -group cat
```
###查找在系统中最后5分钟里修改过的文件
```
find / -mmin -5
```
###查找在系统中最后24小时里修改过的文件
```
find / -mtime -1
```
###查找在系统中属于fred这个用户的文件
```
find / -user fred
```
###查找出大于10000000字节的文件(c:字节，w:双字，k:KB，M:MB，G:GB)
```
find / -size +10000c
```
###查找出小于1000KB的文件
```
find / -size -1000k
```
##使用混合查找方式查找文件
###在/tmp目录下查找大于10000字节并在最后2分钟内修改的文件
```
find /tmp -size +10000c -and -mtime +2
```
###在/目录下查找用户是fred或者george的文件文件
```
find / -user fred -or -user george
```
###在/tmp目录中查找所有不属于panda用户的文件
```
find /tmp ! -user panda
```





