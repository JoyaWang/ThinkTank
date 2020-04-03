# **AFNetworking**

- **AFURLSessionManager**

- **AFHTTPSessionManager**
  - GET登录

  - POST登录

  - 下载

    > 返回存储文件的路径URL
    >
    > 获取进度：对progress的fractionCompleted进行KVO
    >
    > 断点续传

  - 上传



- 当从网络获取数据时，显示菊花

  ```objc
    [[AFNetworkActivityIndicatorManager sharedManager] setEnabled:YES];
  ```

- 设置缓存文件夹名称和缓存大小

  ```objc
  // 设置缓存
      /*
       内存缓存: 5M
       磁盘缓存: 10M
       缓存文件夹名称: joyaImages
       */
      NSURLCache *cache = [[NSURLCache alloc] initWithMemoryCapacity:1024*1024*5 diskCapacity:1024*1024*10 diskPath:@"joyaImages"];
      [NSURLCache setSharedURLCache:cache];
  ```

  