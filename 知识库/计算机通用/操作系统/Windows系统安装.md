# Windows系统安装

用小白装机大师xiaobaixitong.com



Bios - Security - Secure Boot - Disabled



**如果你的BIOS里有这些选项请设置如下：**

Secure Boot 设置为Disabled【禁用启动安全检查，这个最重要】

OS Optimized设置为Others或Disabled【系统类型设置】

CSM(Compatibility Support Module) Support设置为Yes

UEFI/Legacy Boot选项选择成Both

UEFI/Legacy Boot Priority选择成UEFI First





Legacy Boot (传统老式启动）对应硬盘分区表必须为MBR，这种电脑一般只能装32位操作系统。

UEFI Boot（新版电脑启动）对应硬盘分区表必须为GPT（GPT和MBR分区表下都有NTFS格式），这种电脑可以装32位系统，也可以装64位。装64位系统一般对应UEFI Boot和GPT分区表；装32位系统一般对应Legacy Boot和MBR分区表。

如果是32位的系统，必须使bios中能支持legacy boot，并且硬盘要格为MBR分区表。32位的系统，以legacy boot，但是硬盘位GPT，就会卡在win10安装过程中的选盘界面，详细提示“**Windows无法安装，选中的磁盘为GPT分区形式**”，这时就需要用disk genius格盘，选mbr分区。