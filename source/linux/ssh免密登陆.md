# ssh免密登陆

---

> 连接机器 192.168.9.31
> 目标机器 192.168.9.85
> 登陆连接机器，执行脚本

```
ssh-keygen -t rsa
ssh-copy-id -i /root/.ssh/id_rsa.pub root@192.168.9.85
ssh root@192.168.9.85
```




