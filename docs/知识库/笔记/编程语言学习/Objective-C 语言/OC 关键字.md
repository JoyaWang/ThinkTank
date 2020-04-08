# OC 关键字

- @interface 类的声明

- @implementation 类的实现

- @public

  >  默认情况下，对象的属性不允许被外界直接访问，如果允许访问用 @public 关键词

- static

  > 只能修饰方法中的局部变量，变成静态变量，方法完成后不会回收

- self

  - 在对象方法中

    > 父类的成员对于子类来讲，也是属于子类的，所以父类的成员在子类的方法中也可以使用 self

  - 在类方法中

    > 在类方法中，self 指当前类，用来调用当前类的类方法

- 属性访问修饰符

  - private

    > 只能在本类中访问

  - protected

    > 只能在本类和本类的子类中访问
    >
    > 默认是 protected

  - package

    > 当前框架中访问？

  - public

    > 可以在任意地方，通过对象名访问

- @property

  - 在 Xcode 4.4 之前

    > @property 只生成 getter、setter 方法的声明
    >
    > @synthesize： 生成私有属性，并生成 getter、setter 方法的实现

  - Xcode 4.4 开始

    > @property 增强
    >
    > - 自动生成私有属性
    > - 自动生成私有属性的声明和实现
    >   - 声明 _age 变量
    >   - 生成【setter】 - (void) setAge: (Int Age);  声明和实现
    >   - 生成【getter】- (int) age; 声明和实现

  - @property 参数

    - 内存管理相关

      > retain、release

    - 读写相关

      > readwrite 默认值、readonly

    - strong

    - weak

- @synthesize

- instancetype

  > 只能作为方法的返回值，代表返回当前类的对象

- @class

  > 两个头文件相互包含的时候，如果两边都使用 #import 来包含 就会出现 死循环
  >
  > 如 Person 类 import Dog 类，Dog 类 import Person 类
  >
  > 解决办法: 其中 1 个头文件，不要使用 #import 指令，而用 @class 类名;
  >
  > @class Person;
  >
  > 在 .m 文件中再去 #import