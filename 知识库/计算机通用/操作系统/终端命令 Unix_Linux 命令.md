# 终端命令 Unix / Linux Command

查看程序的pid等信息 `ps -ef | grep trojan`

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

 

1、从服务器下载文件
 scp username@servername:/path/filename /tmp/local_destination
 例如scp codinglog@192.168.0.101:/home/kimi/test.txt 把192.168.0.101上的/home/kimi/test.txt
 的文件下载到 /tmp/local_destination
  2、上传本地文件到服务器
 scp /path/local_filename username@servername:/path  
 例如scp /var/www/test.php codinglog@192.168.0.101:/var/www/ 把本机/var/www/目录下的test.php文件
 上传到192.168.0.101这台服务器上的/var/www/目录中

 3、从服务器下载整个目录
   scp -r username@servername:remote_dir/ /tmp/local_dir 
  例如:scp -r codinglog@192.168.0.101 /home/kimi/test  /tmp/local_dir

 4、上传目录到服务器
   scp -r /tmp/local_dir username@servername:remote_dir
   例如：
   scp -r test   codinglog@192.168.0.101:/var/www/  把当前目录下的test目录上传到服务器

   的/var/www/ 目录


### 

## 文件权限查看、更改

![joyawang@Joya-MacBook-Air](操作系统.ftd/joyawang@Joya-MacBook-Air.png)

![各段含义](操作系统.ftd/各段含义.png)

![权限详解](操作系统.ftd/权限详解.png)



在终端运行的程序

Git, Cocoa Pods, Trojan, Nginx, apache, Home brew, Vim



