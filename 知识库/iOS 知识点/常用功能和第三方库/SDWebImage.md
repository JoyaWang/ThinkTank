# SDWebImage

- 常用功能:

- - 图片下载图片缓存
  - 下载进度监听
  - gif处理



- 默认缓存时间: 1周
- 使用的缓存对象: NSCache
- SDImageCache内处理内存警告，以通知的方式，clearMemory



- cleanDisk的执行过程

- - 先遍历所有的缓存文件，记录过期的文件，计算缓存文件的总大小
  - 删除过期的文件
  - 判断macCacheSize的值是否>0,如果大于0再判断缓存文件总大小是否大于maxCacheSize
  - 如果缓存文件的总大小超过maxCacheSize，删除最早的文件

- 最大并发数: 6

- 支持gif

- 怎么判断图片文件的类型的

- - NSData + ImageContentType.m中

  - 根据文件头的第一个字节判断的

  - - case 0xFF (jpg)
    - case 0x89 (png)
    - case 0x47 (gif)
    - case 0x4D (tiff)

- SDWebImage缓存文件的名称

- - 为了防止缓存的图片名称冲突，根据md5计算的
  - md5重复的几率很小很小很小
  - 终端测试echo -n '图片路径' | md5



maxMemoryCost 内存缓存的最大空间

maxMemoryCountLimit 内存缓存的最大数量

maxCacheAge 磁盘缓存存储的最长时间。默认值为1周

maxCacheSize 磁盘缓存的最大空间。默认值为0，不限制占用磁盘大小



 1) loadImage 是 SDWebImage 的核心方法

   2) 图像下载完成后，会自动保存在沙盒中，文件路径是 URL 的 md5

   3) 如果沙盒中已经存在缓存的图像，后续使用 SD 通过 URL 加载图像，都会加载本地沙盒的图像

   4) 不会发起网络请求，同时，回调方法，同样会调用！

   5) 方法还是同样的方法，调用还是同样的调用，不过内部不会再次发起网络请求！

 ***注意*** 如果缓存的图像累计很大，要找后台要接口！