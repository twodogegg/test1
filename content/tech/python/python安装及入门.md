---
title: "Docker 搭建 python 开发环境"
date: 2020-02-22T22:16:08+08:00
draft: true
---

由于本人的 Python 环境被我弄坏了。试了各种办法还是无法挽救。就想到了用docker搭建开发环境
主要有两种方法，一种是制作 python 镜像，一种是用 docker linux 镜像来部署，在linux 系统独立出一套完整的开发环境，然后用 ssh 连接


这里我用的第二种，第二种相对来说安装第三方包的时候更方便一些。 python 镜像的方式，每安装一个新的包就要重新 commit 一下就很麻烦


## 1. 安装untuntu 操作系统 [^1]


1. docker 下载 ubuntu
```
$ docker run -it ubuntu

# 进入linux后
apt-get install openssh-server
```

2. 若出现 `Unable to locate package openssh-service` [^2]

3. 设置ssh-server自动启动

```
> echo 'service ssh start'>>~/.bashrc
```

4. 设置 ssh 登录密码 

```
> passwd
```
我的 1234

5. 安装 `vim` 命令

```
> apt-get install vim
> echo ':set term=builtin_ansi' >> /usr/share/vim/vimrc
```

6. 修改 ssh 配置文件

vim /etc/ssh/sshd_config

```
PermitRootLogin yes  
UsePAM no
```

linux ssh 配置完成

## 2.linux 安装 python3

我安装的版本没有 python3 所以需要自己安装 [^3]

/usr/local/bin/python3

## 3. python pip 加速

使用国内加速可以大幅提高下载速度 [^4]


2. 加


3. docker 构建python 镜像。安装了依赖包以后就 commit 一下，然后再到 pycharm 里面安装配置环境


--- 
[^1]: [安装untuntu 操作系统](https://blog.csdn.net/ambm29/article/details/96483086)
[^2]: [解决 Unable to locate package openssh-service](https://blog.csdn.net/qq_38004174/article/details/87896135)
[^3]: [Ubuntu安装python3.7](https://juejin.im/post/5d5e3891f265da03bf0f48cc)
[^4]: [pip 镜像加速](https://www.cnblogs.com/aimi-cn/p/10746457.html)