# Travis-CI 加密变量

---

## linux安装
```
yum install -y gcc ruby ruby-devel # 安装gcc和ruby环境

gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/ # 改为国内gem源

gem install travis
```

## 登陆github账户
```
travis login --pro

弹出框输入用户名/密码
Username: 用户名
Password for fartherp: 密码
```

## 加密
```
travis encrypt -r owner/repo COVERALLS_TOKEN="secretvalue"

owner：github用户名
repo：github项目仓库名字
```

## 直接在.travis.yml 中添加命令
```
env:
  global:
    - secure: ""
```






