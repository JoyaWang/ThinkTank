# Mac制作Ubuntu启动盘





### 1. 制作系统`.img`



```go
// hdiutil convert -format UDRW -o (.img文件输出全路径) (.iso文件的全路径)
$ hdiutil convert -format UDRW -o Volumes/.../61_Linux/ubuntu-18-04.img Volumes/.../61_Linux/ubuntu-18.04-desktop-amd64.iso
```

### 2. 找到`U盘`挂载的目录

笔者的是 `32G` 的 `U盘`，挂载的路径是 `/dev/disk3`



```php
$ diskutil list 
...
/dev/disk3 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *31.7 GB    disk3
   1:             Windows_FAT_32 NICE                    31.0 GB    disk3s1
...
```

### 3. 取消 `U盘` 的挂载（但是不要拔掉）



```ruby
$ diskutil unmountDisk /dev/disk3
```

### 4. 制作启动盘



```ruby
$ sudo dd if=Volumes/.../61_Linux/ubuntu-18-04.img.dmg of=/dev/rdisk3 bs=1m
```

Tips:

1. 第四步中是 `rdisk3`而不是 `disk3`

