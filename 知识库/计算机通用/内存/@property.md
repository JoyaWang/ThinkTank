# @property

- ### @property 的作用

  @property int age;

  > - 生成一个私有的，int 类型的属性 _age；是声明在 @implementation 的大括弧中
  >
  > - 生成 getter、setter 的声明
  >
  > - 生成 getter、setter 的实现
  >
  >   > setter 的实现: 将传进来的值不做任何操作直接赋值给属性

- ### @property 可以带参数，不同的参数有不同的效果

  - 与多线程相关

    - atomic: 默认的
    - nonatomic:

    > 选择 nonatomic，因为效率高

  - 【MRC下使用】和生成的 set 方法相关的参数

    - retain 生成的 set 方法就是 `标准的 MRC 内存管理代码`，不再是直接赋值了

      而是先判断新旧对象是否为同一个对象，如果不是，release 旧的，retain 新的。

      > retain 只是生成的 set 方法是标准的 MRC 内存管理代码，不会自动的在 dealloc 中 release，所以我们还要在 dealloc 方法中手动的 release 属性指向的对象

      ```objc
      /// 标准的 MRC 内存管理代码
      ///  _dog 属性的 setter 方法
      /// @param dog  用来赋值的 dog 对象
      - (void)setDog:(Dog *)dog {
          // 当赋值的对象和就对象是同一对象时，什么也不做
          if (_dog != dog) // 当新旧对象不是同一对象时, 进行赋值
          {
              // setter 方法的作用: 将传递进来的 dog 对象，赋值给当前对象的 _dog 属性
              // 1. 就对象不再使用，向旧对象发送一条 release 消息
              [_dog release];
              // 2. 使用新对象，向新对象发送一条 retain 消息
              _dog = [dog retain];
          }
      }
      ```

      ```objc
      // retain 不会生成这里的代码，需要手动 release dog
      - (void)dealloc
      {
          // 在此 Person 对象销毁的时候，向持有的 name 和 dog 对象分别发送 release
          // 让 引用计数器 减 1
          [_name release];
          [_dog release];
          [super dealloc];
      }
      ```

    - assign 默认值，生成的 set 方法中不做其他任何操作，直接赋值

    > 如果属性的类型是 OC 对象类型的，使用 retain
    >
    > 如果属性的类型是 非OC 对象类型的，使用 assign

  - 【ARC下使用】strong 、weak

    > 都是应用在 属性的类型 是 OC 对象的时候
    >
    > 大部分时候，都用 strong
    >
    > 只有当出现循环引用的时候，一边用 strong，一边用 weak

  - 和生成的属性 只读、读写 有关的参数

    > readwrite: 默认值， getter setter 同时生成
    >
    > readonly: 只生成 getter

  - 修改生成 getter、setter 方法的名字

    > 一般情况下别改，只在 1 个地方
    >
    > 当属性的类型是 BOOL 类型的时候，就更改 getter 的名字以 is 开头