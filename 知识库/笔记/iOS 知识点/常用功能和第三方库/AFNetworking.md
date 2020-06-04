# AFNetworking 使用

- 获取请求信息和响应信息

  ```objc
  [manager GET:requestUrl parameters:request.requestParams progress:^(NSProgress * _Nonnull downloadProgress) {
          } success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {
              [request requestCompletionCallback:task responseObject:responseObject];
              
              self.infoDict[@"请求URL"] = task.originalRequest.URL;
              self.infoDict[@"请求出错信息"] = error;
              self.infoDict[@"响应体"] = responseObject;
              self.infoDict[@"请求方式"] = task.originalRequest.HTTPMethod;
              NSHTTPURLResponse *rp = (NSHTTPURLResponse *)task.response;
              self.infoDict[@"响应状态码"] = @([rp statusCode]);
              self.infoDict[@"请求头信息"] = task.originalRequest.allHTTPHeaderFields;
              self.infoDict[@"请求正文信息"] = task.originalRequest.allHTTPHeaderFields;
              
          } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
              [request requestFailedCallback:task error:error];
              
              
          }];
  ```

  

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


NSURLSessionDataTask

responseSerializer

AFJSONResponseSerializer 默认初始化器是JSON

[AFHTTPResponseSerializer serializer] 而百度返回的是HTML，所以需要设置为AFHTTPResponseSerializer

responseObject

requestSerializer

AFJSONRequestSerializer serializer

设置请求头