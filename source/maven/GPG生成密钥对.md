﻿# GPG生成密钥对

---

## 安装（版本2.3.4）

Windows 系统，可以下载 Gpg4win 软件来生成密钥对。[https://www.gpg4win.org/download.html](https://www.gpg4win.org/download.html)
推荐使用 Gpg4win-Vanilla 版本，因为它仅包括 GnuPG，这个工具才是我们所需要的。
Linux 系统，直接从源中安装gpg软件包就行。

## gpg/gpg2
> gpg分为gpg和gpg2，需要看自己的maven使用的哪个gpg，再生成对应的gpg密钥。

### window cygwin
```
apt-cyg install gnupg
```

# 如果使用window以下操作在cmd命令行中进行

## 查看是否安装成功
```
gpg --version
```

## 生成密钥对
```
 gpg --gen-key
```

## 查看公钥私钥
```
gpg --list-keys

/home/CK/.gnupg/pubring.gpg
---------------------------
pub   2048R/30509BA4 2017-09-21
uid                  cuiyuqiang (web框架) <yuqiang.cui@gmail.com>
sub   2048R/7B7AA679 2017-09-21
```
其中 **30509BA4** 是需要传到服务器的
## 将公钥发布到 PGP 密钥服务器
```
gpg --keyserver hkp://keyserver.ubuntu.com --send-keys 30509BA4
```
## 查询公钥是否发布成功
```
 gpg --keyserver hkp://keyserver.ubuntu.com --recv-keys 30509BA4
 
 注：使用idea发布代码时，如果退出idea重新登录在发布
```

## 查看密钥
```
gpg --delete-keys id

gpg --delete-secret-key id
```

## git设置全局密钥
```
git config --global user.signingkey 30509BA4
```

