---
layout: wiki
title: Linux常用命令
categories: Linux
keywords: Linux
---

类 Unix 系统下的一些常用命令和用法。

## 实用命令

### fuser

查看文件被谁占用。

```sh
fuser -u .linux.md.swp
```

### id

查看当前用户、组 id。

### lsof

查看打开的文件列表。

> An  open  file  may  be  a  regular  file,  a directory, a block special file, a character special file, an executing text reference, a library, a stream or a network file (Internet socket, NFS file or UNIX domain socket.)  A specific file or all the files in a file system may be selected by path.

#### 查看网络相关的文件占用

```sh
lsof -i
```

#### 查看端口占用

```sh
lsof -i tcp:5037
```

#### 查看某个文件被谁占用

```sh
lsof .linux.md.swp
```

#### 查看某个用户占用的文件信息

```sh
lsof -u mazhuang
```

`-u` 后面可以跟 uid 或 login name。

#### 查看某个程序占用的文件信息

```sh
lsof -c Vim
```

注意程序名区分大小写。


### netstat

#### 查看端口被占用

```sh
netstat -tunlp|grep 80
```

### sudo
* sudo : 暂时切换到超级用户模式以执行超级用户权限，提示输入密码时该密码为当前用户的密码，而不是超级账户的密码。不过有时间限制，Ubuntu默认为一次时长15分钟。
* su ： 切换到某某用户模式，提示输入密码时该密码为切换后账户的密码，用法为“su 账户名称”。如果后面不加账户时系统默认为root账户，密码也为超级账户的密码。没有时间限制。
* sudo -i: 为了频繁的执行某些只有超级用户才能执行的权限，而不用每次输入密码，可以使用该命令。提示输入密码时该密码为当前账户的密码。没有时间限制。执行该命令后提示符变为“#”而不是“$”。想退回普通账户时可以执行“exit”或“logout” 。

### ssh
#### 连接服务器

```sh
sudo -i ssh -p 22 name@host
```

### ps
#### 查看进程号

```sh
ps -ef|grep nginx
```

### tail
* tail -n 100 filename: 查看日志，显示最后1000行
* tail -f -n 100 filename：监视filename文件的尾部100行内容，动态输出在屏幕上
