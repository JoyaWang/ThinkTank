# NSURLSession



- ### 简介

  > - 之前发送网络请求的过程
  >
  >   URL -- URLRequest -- URLConnection
  >
  > - iOS7以后 -- NSURLSession
  >   - 用于替代NSURLConnection
  >   - 支持后台运行的网络任务
  >   - 暂停、停止、重启网络任务，不再需要自己封装NSOperation
  >   - 下载、断点续传、异步下载
  >   - 上传、异步上传
  >   - 获取下载、上传的进度

- ### DataTask

  > 要拿网页HTML数据、JSON、XML数据时使用
  >
  > 【默认挂起，须resume】

- ### UploadTask

  > - 要上传文件时使用
  >
  > - 默认挂起，须resume
  >
  > - 配置Apache服务器WebDav功能
  >
  > - 演示 HTTP 的Method，PUT GET DELETE
  >
  > - PUT 上传
  >
  >   > put直接以文件的方式写入
  >   >
  >   > post需要服务器端脚本支持
  >
  > - 通过session发送put请求上传文件
  >
  >   > 如果直接上传返回状态码401 --没有授权
  >   >
  >   > 因为WebDav设置了基本身份验证，所以请求的时候得携带验证的字符串
  >   >
  >   > 自己上传或删除一个文件，用charles监视请求
  >
  >   请求头有意向Authorization: Basic YWRtaW46MTIzNDU2
  >
  >   YWRtaW46MTIzNDU2是base64编码的账号和密码
  >
  >   通过base64解码还原admin:123456
  >
  > - 常用的请求头
  >
  >   post时候的Content-Type、Range、User-Agent、Authorization 

- ### DownloadTask

  > - 要下载文件时使用
  > - 启动任务--执行的过程是异步的
  > - 默认挂起，须resume
  > - 回调获取文件数据
  > - downloadDelegate获取文件下载进度和实现断点续传，不能使用sharedSession【delegate会出现循环引用】
  >
  > - 会出现的问题
  >
  >   > - 狂点暂停，再继续会闪退
  >   > - 暂停，关闭程序重新开始，继续会闪退
  >   > - 多次点击继续会重复从原来的地方继续下载，所以每点击一次就清空一下resumData
  >
  > - 在界面上放个scrollView，拖动的时候下载任务不会停止
  >
  >   > 因为下载任务是异步执行的(即使把下载任务添加到主队列中)
  >   >
  >   > 当发生合适的事件后，通知代理对象
  >   >
  >   > 所有代理方法都是在主线程上异步执行的(任务添加到主队列的时候)
  >   >
  >   > 拖动scrollView的时候下载不会停止
  >
  > - 内存暴涨的解决办法
  >
  >   > - NSFileHandle
  >   >
  >   >   > 在文件存储的路径，实现下一点，往那个路径存一点的功能
  >   >   >
  >   >   > 还能实现一点一点读的功能？可以解决数组全部加载到内存的问题？
  >   >   >
  >   >   > ```objc
  >   >   > // 为了防止把下载的数据全部加载到内存中，造成内存暴涨闪退，用fileHandle实现下一点往内磁盘存一点，不占用内存
  >   >   > - (void) saveData:(NSData *)data {
  >   >   >     // 创建保存文件的路径
  >   >   >     NSString *filePath = @"/Users/joyawang/Desktop/v.mp4";
  >   >   >     //
  >   >   >     NSFileHandle *handle = [NSFileHandle fileHandleForWritingAtPath:filePath];
  >   >   >     
  >   >   >     if (handle == nil) {
  >   >   >         // 如果此路径还没有文件，先创建文件
  >   >   >         [data writeToFile:filePath atomically:YES];
  >   >   >     } else {
  >   >   >         // 开始处理文件
  >   >   >         // handle offset指针默认指向文件的头部，而我们要往文件的尾部写入数据，所以，先将指针指向尾部
  >   >   >         [handle seekToEndOfFile];
  >   >   >         
  >   >   >         // 写入数据
  >   >   >         [handle writeData:data];
  >   >   >         
  >   >   >         // 关闭处理文件
  >   >   >         [handle closeFile];
  >   >   >     }
  >   >   > }
  >   >   > ```
  >   >   >
  >   >   > 
  >   >
  >   > - NSOutputStream
  >   >
  >   >   > - NSStream 流 抽象类
  >   >   >
  >   >   >   ```objc
  >   >   >   -(void)open;
  >   >   >   -(void)close;
  >   >   >   ```
  >   >   >
  >   >   > - NSOutputStream 输入流
  >   >   >
  >   >   >   - 在内存和硬盘之间创建一个管道，运送一些字节
  >   >   >
  >   >   >   - 把字节通过流写入文件
  >   >   >
  >   >   >     ```
  >   >   >     [write buffer maxLength];
  >   >   >     ```
  >   >   >
  >   >   > - 步骤
  >   >   >   - 接收到响应头开始创建流并打开
  >   >   >   - 接收到数据开始写文件
  >   >   >   - 下载结束或下载出错，关闭流
  >   >   >
  >   >   > - 问题
  >   >   >   - 如果文件已存在，再次下载的时候会追加文件[导致文件比原来大]
  >   >   >   - 在文件下载之前，先判断有文件，如果有则删除重新下载？

- ### NSURLSessionConfiguration

  > 在一个地方配置请求头的信息，所有任务都使用此请求头

  - 作用

    > - 可以设置请求头(Content-Type Range User-Agent Authorization等)
    > - 可以设置最大连接数
    > - 可以设置超时时长，缓存策略

  - 类构造方法

    > - defaultSessionConfiguration
    >
    >   会使用磁盘缓存，账户信息存储到钥匙链，如果有cookie会携带cookie
    >
    > - ephemeralSessionConfiguration
    >
    >   没有磁盘缓存，不存储账户信息，不携带cookie
    >
    >   数据存储在内存，速度快，如果要存储到磁盘须自己写
    >
    > - backgroundSessionConfigurationWithIdentifier
    >
    >   在一个单独的进程上下载
    >
    >   **<u>app进入后台或终止之后，依然可以继续下载</u>**

  - 属性

    > - HTTPAdditionalHeaders 添加请求头
    > - requestCachePolicy 缓存策略
    > - timeoutIntervalForRequest 请求的超时时长
    > - allowsCellularAccess 运行蜂窝网络访问
    > - HTTPMaximumConnectionPerHost 主机的最大连接数

- ### NSURLResponse

  - MIMEType

    > 返回的文件的类型Content-Type

  - ExpectedContentLength

    > 文件的预期大小(实际大小)

  - suggestedFilename

    > 建议保存的文件的名字

