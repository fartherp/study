# github/gitlab同时使用

---
## 初始阶段
```
找到C:\Users\用户\.ssh文件夹。
```

## 生成github ssh key
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com" # github邮箱地址 文件名修改id_rsa_github
将id_rsa_github.pub的内容复制出来，并添加到githab 【settings】中的【SSH keys】中
```

## 生成gitlub ssh key
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com" # gitlub邮箱地址 文件名修改id_rsa_gitlub
将id_rsa_gitlub.pub的内容复制出来，并添加到githab 【settings】中的【SSH keys】中
```

## 添加配置文件
```
# github
Host github.com
	HostName github.com
	IdentityFile ~/.ssh/id_rsa_github
	
#gitlab
Host gitlab
    HostName 192.*.*.*（更改为本地gitlab的ip地址）
    IdentityFile ~/.ssh/id_rsa_gitlub
```

## 启动ssh-agent
```
win 打开服务应用程序
按组合键：win+r 
输入：services.msc
找到 OpenSSH Authentication Agent 启动并设置为自动

win ssh-agent
linux ssh-agent bash
```

## 添加私钥
```
 ssh-add id_rsa_gitlub #添加gitlab私钥
 ssh-add id_rsa_github #添加github私钥
```

## 查看密钥
```
ssh-add -L #查看公钥
ssh-add -l #查看私钥
```

## 配置用户名和邮箱（提交时用）
```
git config --global user.name 'gitlab注册用户名'  # 全局
git config --global user.email 'gitlab注册邮箱'

cd **/github #存放github代码的路径
git config --local user.name 'github注册用户名' # 本地
git config --local user.email 'github注册邮箱'
```

## 测试
```
ssh -T git@192.*.*.*    #gitlab的地址

ssh -T git@github.com
```

## clone项目
```
原本从仓库clone项目的指令是：
git clone git@github.com:fartherp/framework.git

配置中如果 Host github
git clone git@github:fartherp/framework.git
```