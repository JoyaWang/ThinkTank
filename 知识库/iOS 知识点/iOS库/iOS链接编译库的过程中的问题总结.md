# iOS链接编译库的过程中的问题总结



库的问题

1. 如果我添加一个分类,并且公开其头文件,然后在项目中调用会出现奔溃的现象,直接报改调用的方法找不到

   ```
   Terminating app due to uncaught exception 'NSInvalidArgumentException', reason: '-[__NSCFConstantString documentPath]: unrecognized selector sent to instance 0x100fdc008'
   ```

   > 出现原因：由于UNIX的静态库实现、linker和Objective-C的动态结构三者之间的问题引起的。Objective-C并不为每个函数定义linker symbol，它只为每个class生成linker symbol。（objc的动态结构）如果你为一个已存在的class创建了category，那么linker并不知道要将原始class实现和category实现联系起来。这就导致了最终程序中的对象没法响应category中的方法。
   >
   > 解决办法: 在使用库的项目中的Targets中的Build Settings中的Other Linker Flags中添加 -all_load ,然后重新运行。



