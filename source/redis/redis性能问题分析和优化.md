# redis性能问题分析和优化

---

## 内存
```
info memory

used_memory是Redis使用的内存总量，包含了实际缓存占用的内存和Redis自身运行所占用的内存(如元数据、lua)，是由Redis使用内存分配器分配的内存，所以这个数据不包括内存碎片浪费掉的内存，其他字段代表的含义，都以字节为单位。
used_memory_rss：从操作系统上显示已经分配的内存总量。
mem_fragmentation_ratio： 内存碎片率。
used_memory_lua： Lua脚本引擎所使用的内存大小。
mem_allocator： 在编译时指定的Redis使用的内存分配器，可以是libc、jemalloc、tcmalloc。
```

## 延迟时间
```
使用slowlog查出引发延迟的慢命令 slowlog get

1、日志的唯一标识符
2、被记录命令的执行时间点，以 UNIX 时间戳格式表示
3、查询执行时间，以微秒为单位
4、执行的命令，以数组的形式排列。完整命令是config get *
```

## 命令处理数
```
info stats
```

## 持久模式
```
info persistence
```

