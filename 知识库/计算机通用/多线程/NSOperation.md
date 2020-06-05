# NSOperation

> 其实就是要往队列里添加的耗时任务

- ### 简介

  > - OC语言
  > - 基于GCD(底层是GCD)
  > - 比GCD多了一些更简单实用的功能
  > - 使用更加面向对象
  > - 线程生命周期自动管理

- ### 特点

  > - NSOperation是一个抽象类
  > - 不能直接使用(方法只有声明没有实现)
  > - 用来约束子类都具有共同的属性和方法

- ### NSOperation的子类

  > - NSInvocationOperation
  >
  >   > 创建NSInvocationOperation对象
  >   >
  >   > 调用start方法开始执行操作
  >   >
  >   > 默认情况下，调用了start方法后并不会开一条新线程去执行操作，而是在当前线程同步执行，只有将NSOperation放到一个NSOperationQueue中，才会异步执行操作。
  >
  > - NSBlockOperation
  >
  >   > 创建NSBlockOperation对象
  >   >
  >   > 通过addExecutionBlock:方法添加更多操作
  >   >
  >   > 只要NSBlockOperation封装的操作数>1，就会异步执行操作
  >
  > - 自定义operation
  >
  >   > - 即通过创建NSOperation的子类，可以定制一些功能，需要重写main方法，添加自动释放池等
  >   > - 目的: 封装如 `下载图片` 这样的耗时操作
  >   >
  >   > - 自定义Operation，模拟下载图片
  >   >   - 创建HMDownloaderOperation类，继承自NSOperation
  >   >   - 重写自定义Operation的main方法
  >   >   - 重写- (void)main方法，在里面实现想执行的任务
  >   >   - 自己创建**自动释放池**(因为如果是异步操作，无法访问主线程的自动释放池)
  >   >   - 经常通过-(BOOL)isCancelled方法检测操作是否被取消，对取消做出响应
  >   >   - 在controller中调用start方法，或者添加到队列。main方法会被调用

- ### NSOperationQueue 队列

  > 存放并执行操作的地方

- ### 使用步骤

  > 1. 先将需要执行的操作封装到一个 NSOperation 对象中
  > 2. 然后将 NSOperation 对象添加到 NSOperationQueue 中
  >
  > 系统会自动将 NSOperationQueue 中的 NSOperation 取出来执行
  >
  > 将取出来的 NSOperation 封装的操作放到一条新线程中执行

- ### 队列中操作的执行的过程

  > 1. 把操作添加到队列[self.queue addOperationWithBlock];
  > 2. 去线程池取空闲的线程，如果没有就创建新线程
  > 3. 把操作交给从线程池中取出的线程执行
  > 4. 执行完成后，把线程再放回线程池中
  > 5. 重复2,3,4直到所有操作都执行完

- ### 线程间通信

  > 从子线程回到主线程
  >
  > 比如: 当图片在子线程上异步下载完成后回归到主线程上更新UI

  - 主队列

    > 添加到主队列的操作，最终都执行在主线程上

  - 当前队列

    > 获取当前操作的队列
    >
    > [NSOperationQueue currentQueue];

- ### 最大并发数

  > - 什么是最大并发数？
  >
  >   > 最多同时执行的任务数
  >   >
  >   > 比如，同时开3个线程执行3个任务，并发数就是3
  >
  > - 最大并发数的相关方法
  >
  >   > maxConcurrentOperationCount
  >   >
  >   > setMaxtConcurrentOperationCount

- ### 队列的暂停、取消、恢复

  - 取消队列的所有操作

    > cancelAllOperations;
    >
    > 也可以调用NSOperation的cancel方法取消单个操作

  - 暂停和恢复队列

    > setSuspended // YES代表暂停队列，NO代表恢复队列执行
    >
    > isSuspended

- ### 操作的优先级 和 监听操作完成

  > 不设置优先级的话，可以明显看出开了两个线程切换执行op1和op2
  >
  > 
  >
  >  可以设置操作(任务)的优先级(服务质量),但并不能保证高优先级的任务执行过程中，低优先级的任务不执行
  >
  >  op1.qualityOfService = NSQualityOfServiceUserInteractive;
  >
  >  
  >
  >  可以设置监听某个任务完成后回调某个方法
  >
  >  [op1 setCompletionBlock:^{
  >
  >    NSLog(@"-----------------op1 finished--------------");
  >
  >  }];

- ### 操作依赖 (保证任务执行顺序)

  > NSOperation之间可以设置依赖来保证执行顺序
  >
  > 下载、解压和升级完成分别在不同的线程上执行，用add dependency来确保执行顺序
  >
  > 下载和解压操作在子线程，升级完成在主线程执行，依然可以添加依赖。



------

### NSOperation VS GCD

- ### GCD

  > - iOS4.0推出，主要针对多核cpu做了优化，是C语言的技术
  > - GCD是将任务(block)添加到队列(串行/并行/全局/主队列)，并且以同步/异步的方式执行任务的函数
  > - GCD提供了一些NSOperation不具备的功能
  >   - 一次性执行
  >   - 延迟执行
  >   - 调度组

- ### NSOperation

  > - NSOperation是iOS2.0推出的，iOS4之后重写了NSOperation
  >
  > - 将操作NSOperation(异步的任务)添加到队列(并发队列)，就会执行
  >
  > - NSOperation中提供的方便的操作
  >
  >   > - 最大并发数
  >   > - 队列的暂定*/*继续*(*暂停的是没有执行的任务*)*
  >   > - 取消所有的操作
  >   > - 执行操作之间的依赖关系*(GCD*中用同步就可以实现*)*