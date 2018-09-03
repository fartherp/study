# mysql锁表/解锁

---
## 锁表情况
```
show status like 'table%';
Table_locks_immediate  指的是能够立即获得表级锁的次数

Table_locks_waited  指的是不能立即获取表级锁而需要等待的次数
```
## 查看正在被锁定的的表
```
show OPEN TABLES where In_use > 0;
```

## 行锁争用情况
```
show status like 'innodb_row_lock%';
发现锁争用比较严重，如InnoDB_row_lock_waits和InnoDB_row_lock_time_avg的值比较高
```

## 解锁
```
show processlist;
```






