# 终端命令 Unix / Linux Command

提权 `sudo` super user do



光标移到行首 control + a

光标移到行尾 control + e



查看程序的pid等信息 `ps -ef | grep trojan`

> 出现 501 81262 79513  0 4:40PM ttys000  0:00.01 grep trojan

关闭/杀死程序 `kill -9 79513`

开启程序 



### 编辑

- 终端 `control + u` 删除一行命令

### 终止、退出

- 暂停终端当前运行的进程 `Control z`
- 强制退出终端 `Command q`
- 强制退出系统当前运行的某程序 `killall WeChat`

- 退出 man 手册 `q`

- 终止终端当前运行的进程 `Control c` cancel the running process

### 查看IP

- 查看 IP 地址 `ifconfig` en0 wifi地址; en1 ethernet

- 查看局域网所有设备 `arp -a`

- 查看本机与某 IP 地址的机器是否连通 `ping`

- 查看本机到目的地 IP 之间经过多少路由器 `traceroute www.baidu.com`


### 清屏

-  `Control l(L)` `Command k`

语音朗读 `say hi`

反射、重复、回声: `echo "求知若渴，虚心若愚"`



## 目录/文件夹

### 目录快捷键

- 根目录 `/` root directory

- 当前工作目录 `.`


- 当前工作目录的根目录 `./`  比如 `./a.out` 就是当前文件夹中的 a.out 文件


- 家目录、当前用户的根目录 `~`

- 家目录的根目录 `~/`

### 查看目录和切换目录

- 查看当前在哪个目录 `pwd` print working directory


- 切换到某个目录`cd /Users/joyawang/Desktop`

- 切换到上一级文件夹 `cd ..`

- 切换到家目录 `cd`

- 切换到根目录 `cd /`


### 查看目录下的文件和文件夹

- 查看当前文件夹下所有文件和文件夹 `ls` List
- 查看当前文件夹下所有文件和文件夹(包含隐藏文件) `ls -a`

- 查看(详细)当前文件夹下所有文件和文件夹以及权限 `ls -l`

- 查看(详细)当前文件夹下所有文件和文件夹(包含隐藏文件)以及权限 `ls -al`


### 新建、删除、复制文件夹和文件

- 新建文件夹(在当前目录) `mkdir newdirectoryname`
- 删除文件夹 `rmdir directoryname`

- 新建文件 `touch`

- 删除文件 `rm a.txt`

- 复制文件 `cp ~/Desktop/MyFile.rtf ~/Documents`

- 复制文件 `cp -R froshims0 froshims1 `  within same working directory, copy froshims0 directory **and** paste **and** rename to froshims1 within same directory

- 复制文件夹及其中所有内容 `cp -R ~/Desktop/MyFolder /Documents` 




查看文件内容 `cat a.txt`

查看文件内容(分页) `more a.txt` (f,b) Forward下 一页和backword上一页

比较两个文件  `diff` Compares two files line by line (assumes text).

## 文件权限查看、更改

- 更改文件权限 `chmod` change file modes or Access Control Lists


- 更改文件 所有者 和 所有组 `chown` change file owner and group

  `sudo chown -R acme:acme /usr/local/etc/certfiles`

  - `chown` 更改文件的所有者
  - `-R ` 处理指定目录以及其子目录下的所有文件
  - `acme` 新的文件所有者ID
  - `:acme` 新的文件所有者的所属组(group)
  - `/usr/local/etc/certfiles` 要更改的文件

- 更改文件 属组 `chgrp` -- change group


### 创建用户组、用户

- 创建用户组 sudo groupadd certusers

  certusers

  - 申请到证书后将证书所有权交给此用户组
  - 允许此组内用户访问证书

- 创建用户  
  - trojan `sudo useradd -r -M -G certusers trojan`
    - `-r` 系统用户 
    - `-M` 无需登录 
    - 无需家目录
    - `-G certusers` 加入群组
  - acme `sudo useradd -r -m -G certusers acme`
    - `-r`  系统用户
    - `-m` 需要家目录
    - 未设置密码，不能登录，只能通过其他已经登录的用户切换过去
    - 需要读写证书文件，添加到用户组 certusers `-G certusers`

    - `-g<群组> 　指定用户所属的群组`。

    - `-G<群组> 　指定用户所属的附加群组。`

    - `-m 　自动建立用户的登入目录。`

    - `-M 　不要自动建立用户的登入目录。`

    - `-n 　取消建立以用户名称为名的群组．`

    - `-r 　建立系统帐号。`

  

在终端运行的程序

Git, Cocoa Pods, Trojan, Nginx, apache, Home brew, Vim



