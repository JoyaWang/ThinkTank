# Mac格式化U盘

Found the answer - diskutil at the command line.



My USB drive shows up in "diskutil list" as:



/dev/disk4 (external, physical):

   \#:                       TYPE NAME                    SIZE       IDENTIFIER

   0:     FDisk_partition_scheme                        *62.7 GB    disk4

   1:                       0xEF                         9.2 MB     disk4s2



I think the problem is the partitioning scheme.  To erase the device completely, I just ran:



```shell
diskutil eraseDisk free EMPTY /dev/disk4

diskutil list
```



/dev/disk4 (external, physical):

   \#:                       TYPE NAME                    SIZE       IDENTIFIER

   0:      GUID_partition_scheme                        *62.7 GB    disk4

   1:                        EFI EFI                     209.7 MB   disk4s1



Much better... it now has a partitioning scheme MacOs can work with.  At this stage, you won't see it showing in the Disk Utility program, but fortunately formatting it is trivial.  I decided to use ExFAT, and name the drive USB64:



```shell
diskutil eraseDisk ExFAT USB64 /dev/disk4
```



/dev/disk4 (external, physical):

   \#:                       TYPE NAME                    SIZE       IDENTIFIER

   0:      GUID_partition_scheme                        *62.7 GB    disk4

   1:                        EFI EFI                     209.7 MB   disk4s1

   2:       Microsoft Basic Data USB64                   62.5 GB    disk4s2



And now I have a fully working USB drive again!



TIP:  if ExFAT isn't your thing... there are of course other filesystems available.  To see them, run:



diskutil listFilesystems