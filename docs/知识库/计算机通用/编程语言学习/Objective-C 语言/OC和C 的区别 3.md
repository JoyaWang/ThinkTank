# OC 和 C 的区别

OC 在C 的基础上新增了1小部分面向对象的语法

OC 程序的源文件后缀名是 .m, m 岱庙 message 代表 OC 中最重要的1个机制 消息机制

main 函数仍然是 OC 程序的 入口和出口

- #import 指令

  - 以 # 开头，是个 预处理指令
  - 作用: 是 #include 的增强版，将文件的内容在预编译的时候拷贝到写指令的地方
  - 增强: 同1个文件无论 #import 多少次，只会包含1次，如果 #include 指令要实现此效果，必须配合条件编译指令来实现
  - 原理: import时底层会判断是否已经包含

- 框架

  - 是1个功能集合 苹果或者第三方事先将一些在程序开发时会用到的功能事先写好，把这些功能封装在1个个类或者函数中，这些函数和类的集合就叫做框架

  - 有点像 C 语言的函数库

  - Foundation 框架

    > Foundation.h这个文件中包含了 Foundation 框架中的其他的所有头文件，只需要包含 Foundation.h，就相当于包含了 Foundation 框架中所有头文件，
    >
    > Foundation 框架中所有类和函数都可直接使用

- NSLog

- 字符串 NSString

- NS 前缀

- OC 程序的编译、链接、执行

  - 在.m文件中写上符合OC语法的源代码

  - 使用编译器将源代码编译为目标文件

    > cc -c xx.m
    >
    > - 预处理
    > - 检查语法
    > - 编译

  - 链接

    > cc main.o
    >
    > - 如果程序中用到了框架中的函数或类，那么在链接时，必须告诉编译器去哪个框架中找这个函数或者类
    >
    > cc xx.o -framework Foundation

  - 链接成功后，就会生成 a.out 可执行文件，执行就可以了

- 我们点击运行按钮，所有的事情 Xcode 都自动帮我们做了 

- ### OC 中的数据类型

  - OC 中支持C语言中的所有数据类型

    - 基本数据类型

      > int double float char

    - 构造类型

      > 数组、结构体、枚举

    - 指针类型

      > int *p1

    - 空类型

      > void

    - typedef 自定义类型

  - BOOL 类型

    - 可以存储 YES 或者 NO 的任意一个数据
    - 一般情况下 BOOL 类型的变量用来存储条件表达式的结果

  - Boolean

  - class 类型， 类

  - id 类型 万能指针

  - nil 与 NULL 差不多

  - SEL 方法选择器

  - block 代码段

- OC 的运算符

- OC 的控制语句

- OC 中的关键字

  - OC 支持 C 语言中的全部关键字，并且效果一致
  - OC 新增一些关键字，绝大多数以 @ 开头
    - @interface
    - @implementation
    - @public
  - 函数的定义和调用与 C 语言完全一致

  