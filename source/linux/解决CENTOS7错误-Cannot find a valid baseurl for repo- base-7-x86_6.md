# 解决CENTOS7错误:Cannot find a valid baseurl for repo: base/7/x86_6

---

## 解决方案
```
vi /etc/sysconfig/network-scripts/ifcfg-eth0 （每个机子都可能不一样，但格式会是“ifcfg-eth数字”），把ONBOOT=no，改为ONBOOT=yes
重启网络：service network restart
```

## 装个图形界面
```
yum groupinstall -y "GNOME Desktop" "Graphical Administration Tools"
```




