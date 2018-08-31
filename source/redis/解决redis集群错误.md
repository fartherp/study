# 解决redis集群错误

---

## CLUSTERDOWN The cluster is down

## Ruby在线安装
```
sudo yum install ruby    # CentOS, Fedora, 或 RHEL 系统
sudo apt-get install ruby-full # Debian 或 Ubuntu 系统

brew install ruby  # 苹果系统
```

## RVM升级Ruby  
```
ruby -v  # 查看当前ruby版本

vim /usr/local/rvm/user/db

ruby_url=https://cache.ruby-china.org/pub/ruby # 利用国内镜像

rvm -v # 测试是否安装正常


rvm list known # 列出已知ruby的版本

rvm install 2.4 # 安装ruby 2.4，rvm会自行寻找此版本
```

## 安装redis插件
```
gem install redis
```

## 检查redis集群
```
./redis-trib.rb check 192.168.16.102:20010
```

## 解决错误
```
./redis-trib.rb fix 192.168.16.102:20010
```





