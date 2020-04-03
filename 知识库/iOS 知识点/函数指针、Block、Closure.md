# 函数指针、Block、Closure的使用

- ### 函数指针

  - 函数的声明

    > 返回值类型 函数名称([参数列表])
    >
    > {
    >
    > ​	写上那段需要被重用的代码；
    >
    > ​	叫做函数体
    >
    > }

  - 指向函数的指针

    - 声明

      > 返回值类型 (*指针名) ([参数列表]);
      >
      > - void (*pFunction) ();
      >
      >   > 表示声明了1个指向函数的指针，名字叫做pFunction。
      >   >
      >   > 这个指针只能指向没有返回值，并且没有参数的函数。
      >
      > - int (*pFun) (int num1, int num2);
      >
      >   > 表示声明了1个指向函数的指针，名字叫做pFun.
      >   >
      >   > 这个指针只能指向返回值为int类型，并且有两个整型的参数的函数。

    - 初始化

      > 1. 取到符合指针条件的函数的地址
      >
      >    > 函数的名称就代表函数的地址
      >
      > 2. 将地址赋值给指针变量
      >
      >    > 直接将符合条件的函数的名称赋值给这个指针。

    - 使用指针间接调用指针指向的函数

      ```c
      void (*pFunc) () = test; // pFunc指针就指向了test函数
      pFunc();
      (*pFunc)();
      ```

      

- ### Block (OC)

  - OC中 `方法` 的声明

    ```objc
    -(void) demo:(NSString *)name {
      function body;
    }
    ```

  - OC 中声明 `block` 类型的 `变量`

    > 返回值类型 (^block名称)(参数);
    >
    > void (^demo)();
    >
    > void (^finishedBlock)(UIImage *image);

  - OC 中声明 block 类型的 `属性`

    ```swift
    // Block类型的属性：当网络任务完成时的回调block
    @property (nonatomic, copy) void (^finishedBlock)(UIImage *image);
    ```

  - OC  中声明 block 类型的 `函数参数`

    ```objc
    // 接收block参数的类方法
    + (instancetype) operationWithURLString:(NSString *)urlString andFinishedBlock:(void (^)(UIImage *image)) finishedBlock;
    ```

  - OC 中 block 的初始化

    ```objc
    // 在Xcode中输入inlineblock就会出现
    void (^demo)() = ^(参数) {
    	NSLog(@"快快快");
    };
    
    [self setDemo:^{
        NSLog(@"快快快");
     }];
    ```

  - OC 中 block 的调用

    > demo();

  

- ### Closure (Swift)

  - Swift 中 函数/方法 的声明

    > func demo(_ name: Int) -> Void {
    >
    > 代码
    >
    > }

  - Swift 中声明 closure 类型的变量

    ```swift
    /// 记录显示 VC 的闭包
        var competionBlock:((_ clsName:String?)->())?
    ```

    > (参数)->(返回值类型)

  - Swift 中声明 closure 类型的函数参数

    ```swift
    func tokenRequest(method:JLHTTPMethod = .GET,
                          URLString:String,
                          parameters:[String:Any]?,
                          name:String? = nil,
                          data:Data? = nil,
                          completion: @escaping (_ json:Any?, _ isSuccess:Bool)->()){
                          
    }
    
    class func loadStatus(since_id:Int64 = 0, 
                          max_id:Int64 = 0, 
                          completion: @escaping (_ list:[[String:Any]]?, _ isSuccess:Bool)->()){
      
    }
    ```

  - Swift 中 closure 的初始化

    ```swift
    // 完整写法
    alphaAnim.completionBlock = {(anim, isSuccess)->() in
                        // 需要执行回调
                        print("完成回调展现控制器")
                        self.competionBlock?(sender.clsName)
                    }
    // 简写
    alphaAnim.completionBlock = {_, _ in
                        // 需要执行回调
                        print("完成回调展现控制器")
                        self.competionBlock?(sender.clsName)
                    }
    ```

    

