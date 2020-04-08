## NSFileManager 文件管理器

> 【像Finder一样管理文件】

- 初始化

  > [NSFileManager defaultManager]

- 判断

  - 判断指定文件或文件夹是否存在

    > fileExistsAtPath

  - 判断指定文件夹是否可读取

    > isReadableFileAtPath

  - 判断指定文件夹或文件是否可写入

    > isWriteableFileAtPath

  - 判断指定文件夹或文件是否可删除

    > isDeleteableFileAtPath

- 获取信息

  - 获取指定文件夹或文件的属性信息

    > attributesOfItemAtPath

  - 获取指定路径下的所有文件和目录，所有子目录和文件

    > subpathsAtPath

  - 获取指定路径的所有子目录和文件，不包括孙子辈

    > contentsOfDirectoryAtPath

- 文件 / 文件夹操作

  - 在指定目录创建文件

    > createFileAtPath

  - 在指定目录创建文件夹

    > createDirectoryAtPath

  - 拷贝文件

    > copyItemAtPath toPath

  - 移动文件(剪切文件，可用来重命名)

    > moveItemAtPath toPath

  - 删除文件(不倒废纸篓，直接删除，谨慎使用)

    > removeItemAtPath