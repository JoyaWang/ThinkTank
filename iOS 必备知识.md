# iOS 必备知识

### 内存管理

- ARC 和 MRC 的区别    
- 属性的关键字，他们具体的底层实现以及区别，被问烂的知识点包括 copy， 浅拷贝和深拷贝的区别， weak 的底层实现。稍微新颖一点的 assgin 和 weak，unsafe_unretained 具体有什么区别，assgin是否可以用来修饰对象。这一部分是面试必问，一定要弄懂。    
- Autorelease pool的底层实现原理，与 Runloop 的关系， autoreleasing 关键字。



### Block

- 本质，基础概念
- 使用时要注意的地方
- block的实现，如何截获自动变量的，如何修改自动变量的值的，block的几种形式
- __block的本质
- forwarding 指针
- block怎么避免循环引用。是不是所有的block都会产生循环引用，block里面怎么避免被提前释放



### 多线程

- iOS 中多线程的几种方式，区别，使用场景，基本概念，同步异步，串行并行的区别。
- GCD，写一个死锁，并行和串行队列，同步和异步的区别，GCD怎么控制最大并发数
- 怎么让子线程定时执行一个方法，具体的实现方法
- 如何控制线程的最大并发数为10，然后加载十个图片最后展示出来，具体方法
- 子线程的runloop是怎么执行的，它里面的 autoreleasepool 是怎么执行的。
- NSMutableArray 怎么保证线程安全的。
- GCD怎么避免block中的变量被提前释放



### Runtime

- 消息的动态转发
- 给 Category 添加属性，关联对象都有几种形式
- method swizzling
- 说一说类的结构，运行时中的class都有什么属性，property都有什么属性
- 说一说isa指到NSObject的那个过程
- Category的本质，load方法什么时候加载，Category重写了父类的方***怎样，底层源码 ，如果两个Category和一个基类，都有同名方法，先执行哪个
- property会自动生成什么，如果此时已经有下划线_name的实例变量了那会生成什么
- load 和 initialize



### Runloop

- runloop实现原理
- source 类型
- 线程保活的方式
- runloop和多线程的关系，以及timer的关系



### 第三方库的源码



### 生命周期

- app 的声生命周期
- 控制器的生命周期
- 视图的生命周期



### UI

- UICellectionView 瀑布流
- UITableView 相关的优化，底层原理等
- 页面布局
- layoutSubviews 和 drawRect 等的区别
- 自己实现一个 UIScrollView
- 事件的传递链和响应链
- 界面非常卡顿怎么定位到具体的类和方法
- UIView 和 CALayer 区别



### 数据存储

- 数据持久化都有什么，用过什么，归档，偏好设置都可以存储什么类型



### 架构

- MVC、MVVM
- 从 0 到 1 实现一个 app 的思路
- 对于项目从 main 函数执行之前到之后启动优化，卡顿优化和界面优化



### OC 语言特性

- OC 和 C 的区别， OC 和 Java、C++ 的区别
- iOS 中的协议
- OC 动态性
- C 语言如何动态的交换两个方法的实现



### 其他

- KVO 的底层原理，自己实现
- KVC 的底层原理，自己实现
- NSNotification 的底层原理，是同步还是一部，如何实现一个，如果在子线程接收一个通知能不能接收到
- 几种页面传值方式的区别
- 界面非常卡顿怎么定位到具体的类和方法
- 一个 int 类型的值，被 @ 包装成 NSNumber 类型，传递到一个接受 id 类型的方法参数中，这个值能不能保持正确
- 在 iPad 上面，分屏功能，拖拽 wps 的文件到 qq 的过程是怎么实现的 (进程间通信的方法)
- 如何实现 dispatch_once
- Instrument 的使用
- 热修复用过吗，平时版本怎么迭代，线上 bug 怎么修复？



### 必备书单 

- ​    图解 TCP/IP, 图解 HTTP    
- ​    剑指offer    
- ​    Effective Objective-C    
- ​    iOS 与 OSX 高级编程    
- ​    以上都是必须要重复看很多遍的书单，其他不太重要的暂不列出