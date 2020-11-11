# java查看CPU100%

```
查看哪个PID占用CPU 100%：top
进程的栈dump到文件：jstack -F 进程PID > cpu_100.log
查看进程哪些线程在占用cpu：top -H -p 进程PID 
查看日志: vi cpu_100.log
```
