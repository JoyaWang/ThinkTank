# Linux系统服务器下载、上传目录和文件

### 1、从服务器下载文件

```powershell
scp username@servername:/path/filename /tmp/local_destination
```

 例如scp codinglog@192.168.0.101:/home/kimi/test.txt 把192.168.0.101上的/home/kimi/test.txt
 的文件下载到 /tmp/local_destination

###   2、上传本地文件到服务器

```shell
scp /path/local_filename username@servername:/path
```

例如scp /var/www/test.php codinglog@192.168.0.101:/var/www/ 把本机/var/www/目录下的test.php文件
 上传到192.168.0.101这台服务器上的/var/www/目录中 

### 3、从服务器下载整个目录

```shell
scp -r username@servername:remote_dir/ /tmp/local_dir 
```


  例如:scp -r codinglog@192.168.0.101 /home/kimi/test  /tmp/local_dir

###  4、上传目录到服务器

```shell
scp -r /tmp/local_dir username@servername:remote_dir
```


   例如：
   scp -r test   codinglog@192.168.0.101:/var/www/  把当前目录下的test目录上传到服务器

   的/var/www/ 目录