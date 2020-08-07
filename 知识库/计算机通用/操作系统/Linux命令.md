# Linux命令

[The Linux Command Line 英文](http://linuxcommand.org/lc3_lts0020.php)

[The Linux Command Line 中文](https://www.kancloud.cn/thinkphp/linux-command-line/39431)

control + a 光标移到行首 

control + e 光标移到行尾 

netstat -aptn 命令行，查看所有开启的端口号

lsof -i:端口号 命令行，以80为例

ctrl + u 删除一行命令

ctrl + c 终止终端当前运行的进程 cancel the running process

ctrl + z 暂停终端当前运行的进程 

ctrl + l(L) 清屏

cmd + k 清屏

killall WeChat 关闭/杀死程序

kill -9 79513 关闭/杀死程序

su joyawangchina 切换用户

passwd joyawangchina 设置密码



cat a.txt 查看文件内容 

more a.txt 查看文件内容(分页)  (f,b) Forward下 一页和backword上一页

diff xxx xxx 比较两个文件Compares two files line by line (assumes text)

**cat /proc/cpuinfo **查看linux系统的CPU型号、类型以及大小

**cat /proc/meminfo** 查看linux系统内存大小的详细信息，可以查看总内存，剩余内存、可使用内存等信息



/ 根目录root directory

. 当前工作目录

./ 当前工作目录的根目录, 比如 ./a.out 就是当前文件夹中的 a.out 文件

~ 当前用户的根目录,家目录

~/ 家目录的根目录

pwd 查看当前在哪个目录 print working directory

cd 切换到某个目录

cd .. 切换到上一级文件夹

cd ~ 切换到家目录

cd / 切换到根目录

ls 查看当前文件夹下所有文件和文件夹 List

ls -a查看当前文件夹下所有文件和文件夹(包含隐藏文件) 

ls -l 查看(详细)当前文件夹下所有文件和文件夹以及**权限** 

ls -al 查看(详细)当前文件夹下所有文件和文件夹(包含隐藏文件)以及权限

mkdir xxx 新建文件夹(在当前目录) 

rmdir xxx 删除空文件夹 

rm -rf xxx 删除文件夹(非空也可以) 

touch xxx 新建文件 

rm xxx 删除文件

cp xxx xxx 复制文件

cp -R froshims0 froshims1复制文件  within same working directory, copy froshims0 directory **and** paste **and** rename to froshims1 within same directory

cp -R xxx xxx 复制文件夹及其中所有内容 

ifconfig 查看 IP 地址 en0 wifi地址; en1 ethernet

arp -a 查看局域网所有设备

ping 查看本机与某 IP 地址的机器是否连通

traceroute www.baidu.com 查看本机到目的地 IP 之间经过多少路由器





创建用户组 certusers

sudo groupadd certusers

> 申请到证书后将证书所有权交给此用户组，允许此组内用户访问证书

创建用户 trojan

sudo useradd -r -M -G certusers trojan

> -r 代表系统用户
>
> -M 无需登录
>
> 没有-m，不需要家目录
>
> -G certusers 将此用户加入用户组 certusers

创建用户 acme

sudo useradd -r -m -G certusers acme

> -r 代表系统用户
>
> -m 需要家目录
>
> 未设置密码，不能登录，只能通过其他已经登录的用户切换过去
>
> -G certusers 添加到用户组 certusers，将用于此组所具有的权限，比如读写证书文件

> -g<群组> 　指定用户所属的群组
>
> -G<群组> 　指定用户所属的附加群组
>
> -m 自动建立用户的登入目录
>
> M 不要自动建立用户的登入目录
>
> -n 取消建立以用户名称为名的群组
>
> -r 建立系统帐号



### chmod 更改文件权限  

> change file modes or Access Control Lists
>
> 更改文件 9 个属性 chmod

> `chmod u=rwx,g=rx,o=r test1` 即将 test1 文件权限修改为 **-rwxr-xr--**
>
> - u user
>
> - g group
>
> - o others

> `chmod +x ./Desktop/test.sh`给test.h文件添加可执行权限  

> 语法：chmod abc file
> 引用地址:[https://blog.csdn.net/my_wade/article/details/47066905](https://links.jianshu.com/go?to=https%3A%2F%2Fblog.csdn.net%2Fmy_wade%2Farticle%2Fdetails%2F47066905)
> 其中a,b,c各为一个数字，a表示User，b表示Group，c表示Others的权限。
>
> r=4，w=2，x=1
>
> 若要rwx（可读、可写、可执行）属性，则4+2+1=7
>
> 若要rw-（可读、可写、不可执行）属性，则4+2=6
>
> 若要r-w（可读、不可写、可执行）属性，则4+1=5
>  范例：
>
> `chmod a=rwx file` 和 `chmod 777 file` 效果相同
>
> `chmod ug=rwx,o=x file` 和 `chmod 771 file` 效果相同
>
> 若用`chmod 4755 filename`可使此程式具有root的权限



### chown 更改文件 所有者 和 所有组 

> change file owner and group

`sudo chown -R acme:acme /usr/local/etc/certfiles`

> - `chown` 更改文件的所有者
> - `-R ` 处理指定目录以及其子目录下的所有文件
> - `acme` 新的文件所有者ID
> - `:acme` 新的文件所有者的所属组(group)
> - `/usr/local/etc/certfiles` 要更改的文件



### chgrp 更改文件属组

> change group



## 查看程序的pid等信息

`ps -ef | grep trojan`  

> 出现 501 81262 79513  0 4:40PM ttys000  0:00.01 grep trojan

> `-e` and `-f` are options to the `ps` command, and pipes take the output of one command and pass it as the input to another. Here is a full breakdown of this command:
>
> ps - list processes
>
> -e - show all processes, not just those belonging to the user
>
> -f - show processes in full format (more detailed than default)
>
> command 1 | command 2 - pass output of command 1 as input to command 2
>
> grep find lines containing a pattern. grep (global search regular expression(RE) and print out the line,全面搜索正则bai表达式du并把行打zhi印出来)是一种强大的文本dao搜索工具，它能使用正则表达式搜索文本，并把匹配的行打印出来。
>
> processname - the pattern for grep to search for in the output of ps -ef
>
> So altogether
>
> ```
> ps -ef | grep processname
> ```
>
> means: look for lines containing `processname` in a detailed overview/snapshot of all current processes, and display those lines