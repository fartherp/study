# mongodb导入导出
## 导出
```
-h,--host ：代表远程连接的数据库地址，默认连接本地Mongo数据库；
--port：代表远程连接的数据库的端口，默认连接的远程端口27017；
-u,--username：代表连接远程数据库的账号，如果设置数据库的认证，需要指定用户账号；
-p,--password：代表连接数据库的账号对应的密码；
-d,--db：代表连接的数据库；
-c,--collection：代表连接数据库中的集合；
-f, --fields：代表集合中的字段，可以根据设置选择导出的字段；
--type：代表导出输出的文件类型，包括csv和json文件；
-o, --out：代表导出的文件名；
-q, --query：代表查询条件；
 --skip：跳过指定数量的数据；
--limit：读取指定数量的数据记录；
--sort：对数据进行排序，可以通过参数指定排序的字段，并使用 1 和 -1 来指定排序的方式，其中 1 为升序排列，而-1是用于降序排列,如sort({KEY:1})。

注意：
　　当查询时同时使用sort,skip,limit，无论位置先后，最先执行顺序 sort再skip再limit。
　　
样例：
mongoexport.exe -h 192.168.1.1 --port 27017 -u test -p test -d test -c test --type=json -o C:\Users\risk\Desktop\test.json
```

## 导入
```
h,--host ：代表远程连接的数据库地址，默认连接本地Mongo数据库；
--port：代表远程连接的数据库的端口，默认连接的远程端口27017；
-u,--username：代表连接远程数据库的账号，如果设置数据库的认证，需要指定用户账号；
-p,--password：代表连接数据库的账号对应的密码；
-d,--db：代表连接的数据库；
-c,--collection：代表连接数据库中的集合；
-f, --fields：代表导入集合中的字段；
--type：代表导入的文件类型，包括csv和json,tsv文件，默认json格式；
--file：导入的文件名称
--headerline：导入csv文件时，指明第一行是列名，不需要导入；

样例：
mongoimport.exe -h 192.168.1.1 --port 27017 -u test -p test -d test -c test --type=json --file D:\\test.json
```