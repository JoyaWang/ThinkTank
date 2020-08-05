

## iOS库的介绍

- ### 开源库

- ### 闭源库

  > .a是一个纯二进制文件，.framework中除了有二进制文件之外还有资源文件。.a，要有.h文件以及资源文件配合，.framework文件可以直接使用。总的来说，.a + .h + sourceFile = .framework。所以创建静态库最好还是用.framework的形式。

  - 动态库

    > 动态库即动态链接库（Windows 下的 .dll，Linux 下的 .so，Mac 下的 .dylib/.tbd）

    > 与静态库相反，动态库在编译时并不会被拷贝到目标程序中，目标程序中只会存储指向动态库的引用。等到程序运行时，动态库才会被真正加载进来。
    >
    > 动态库的优点是，不需要拷贝到目标程序中，不会影响目标程序的体积，而且同一份库可以被多个程序使用（因为这个原因，动态库也被称作**共享库**）。同时，编译时才载入的特性，也可以让我们随时对库进行替换，而不需要重新编译代码。动态库带来的问题主要是，动态载入会带来一部分性能损失，使用动态库也会使得程序依赖于外部环境。如果环境缺少动态库或者库的版本不正确，就会导致程序无法运行（Linux 下喜闻乐见的 lib not found 错误）。
    >
    > 系统动态库：链接时不复制，程序运行时由系统动态加载到内存，供程序调用，系统只加载一次，多个程序共用，节省内存

  - 静态库 

    > 静态库即静态链接库（Windows 下的 .lib，Linux 和 Mac 下的 .a)

    > 链接时，静态库会被完整地复制到可执行文件中，被多次使用就有多份冗余拷贝
    >
    > 是因为静态库在编译的时候会被直接拷贝一份，复制到目标程序里，这段代码在目标程序里就不会再改变了。
    >
    > 静态库的好处很明显，编译完成之后，库文件实际上就没有作用了。目标程序没有外部依赖，直接就可以运行。当然其缺点也很明显，就是会使用目标程序的体积增大。
    >
    > 用户拿到的文件有很多头文件.h 和 资源包 和 编译过的二进制文件 .a即没有公开的那些文件被编译进了.a或.framework里面。

  - iOS Framework

    > 除了上面提到的 .a 和 .dylib/.tbd 之外，Mac OS/iOS 平台还可以使用 Framework。Framework 实际上是一种打包方式，将库的二进制文件，头文件和有关的资源文件打包到一起，方便管理和分发。
    >
    > 在 iOS 8 之前，iOS 平台不支持使用动态 Framework，开发者可以使用的 Framework 只有苹果自家的 UIKit.Framework，Foundation.Framework 等。这种限制可能是出于安全的考虑（见[这里的讨论](https://link.jianshu.com?t=https://stackoverflow.com/questions/4733847/can-you-build-dynamic-libraries-for-ios-and-load-them-at-runtime))。换一个角度讲，因为 iOS 应用都是运行在沙盒当中，不同的程序之间不能共享代码，同时动态下载代码又是被苹果明令禁止的，没办法发挥出动态库的优势，实际上动态库也就没有存在的必要了。
    >
    > 由于上面提到的限制，开发者想要在 iOS 平台共享代码，唯一的选择就是打包成静态库 .a 文件，同时附上头文件（例如[微信的SDK](https://link.jianshu.com?t=https://open.weixin.qq.com/cgi-bin/showdocument?action=dir_list&t=resource/res_list&verify=1&id=open1419319164&token=&lang=zh_CN)）。但是这样的打包方式不够方便，使用时也比较麻烦，大家还是希望共享代码都能能像 Framework 一样，直接扔到工程里就可以用。于是人们想出了各种奇技淫巧去让 Xcode Build 出 iOS 可以使用的 Framework，具体做法参考[这里](https://link.jianshu.com?t=https://github.com/kstenerud/iOS-Universal-Framework)和[这里](https://link.jianshu.com?t=https://github.com/jverkoey/iOS-Framework)，这种方法产生的 Framework 还有 “伪”(Fake) Framework 和 “真”(Real) Framework 的区别。
    >
    > iOS 8/Xcode 6 推出之后，iOS 平台添加了动态库的支持，同时 Xcode 6 也原生自带了 Framework 支持（动态和静态都可以），上面提到的的奇技淫巧也就没有必要了（新的做法参考[这里](https://link.jianshu.com?t=http://www.cocoachina.com/ios/20141126/10322.html)）。为什么 iOS 8 要添加动态库的支持？唯一的理由大概就是 Extension 的出现。Extension 和 App 是两个分开的可执行文件，同时需要共享代码，这种情况下动态库的支持就是必不可少的了。但是这种动态 Framework 和系统的 UIKit.Framework 还是有很大区别。系统的 Framework 不需要拷贝到目标程序中，我们自己做出来的 Framework 哪怕是动态的，最后也还是要拷贝到 App 中（App 和 Extension 的 Bundle 是共享的），因此苹果又把这种 Framework 称为[Embedded Framework](https://link.jianshu.com?t=https://developer.apple.com/library/prerelease/ios/documentation/General/Conceptual/ExtensibilityPG/ExtensionScenarios.html)。









