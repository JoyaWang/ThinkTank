# 库支持的CPU架构、链接库的参数、打印环境变量

## iOS的CPU架构

iOS测试分为模拟器测试和真机测试，处理器分为32位和64位处理器

> 使用 lipo -info /Users/joyawang/OCAdditionsFrame 查看库支持的架构

- 模拟器架构

  - i386架构 

    模拟器32位处理器测试，（iphone5,iphone5s以下的模拟器）

  - **x86_64架构** 

    模拟器64位处理器测试，(iphone6以上的模拟器)

- 真机架构

  - armv7,或者armv7s架构 

    真机32位处理器（iphone4真机/armv7,    ipnone5,iphone5s真机/armv7s）

  - **arm64架构** 

    真机64位处理器需要。(iphone6,iphone6p以上的真机)

### project -> target -> building setting -> Arhitectures 设置

 debug属性设置为no的时候，会编译支持所有架构的版本，编译的速度会变慢，设置为yes 的时候，只编译当前的architecture版本，编译速度快。

一般情况下，debug 设置为yes，release为no，这样发行版本能适应不同设备。



## 链接库的参数

### 在Build Settings-Linking-Other Linker Flags



**-ObjC**

这个flag告诉链接器把库中定义的Objective-C类和Category都加载进来。这样编译之后的app会变大（因为加载了其他的objc代码进来）。但是如果静态库中有类和category的话只有加入这个flag才行。



**-all_load**

这个flag是专门处理-ObjC的一个bug的。用了-ObjC以后，如果类库中只有category没有类的时候这些category还是加载不进来。变通方法就是加入-all_load或者-force-load。-all_load会强制链接器把目标文件都加载进来，即使没有objc代码。

注意：假如你使用了不止一个静态库文件，然后又使用了这个参数，那么你很有可能会遇到ld: duplicate symbol错误，因为不同的库文件里面可能会有相同的目标文件



**-force_load**

这个flag所做的事情跟-all_load其实是一样的，只是 -force_load 需要指定要进行全部加载的库文件的路径，这样的话，你就只是完全加载了一个库文件，不影响其余库文件的按需加载 ，-force_load在xcode3.2后可用。

-force_load $(BUILT_PRODUCTS_DIR)/MJExtension/libMJExtension.a



## 打印所有环境变量

在**Xcode**: View > Navigators > Show Report Navigator查看

 在Build phases 中点+创建一个Script，里面写上env，就可打印环境变量出来，可以Command+9去那里看

$(inherited)表示

```
$(TARGET_NAME) Target project name
```

${PODS_ROOT}

$(SRCROOT)  

The path to the project file (such as Nuno.xcodeproj)

项目根目录下【cloudExchange Project的根目录，比如qiyu手动添加的frameworks所在的位置】

$(PROJECT_DIR) 整个项目(工程)的根目录

$(BUILT_PRODUCTS_DIR)