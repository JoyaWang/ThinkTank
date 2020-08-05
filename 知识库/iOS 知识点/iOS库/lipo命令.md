# lipo命令



### lipo -info xxx 查看库支持的CPU架构

```
lipo -info LoginSDK.a
```



### lipo -create xxx xxx -output xxx 合成支持不同CPU架构的库

```
lipo -create /Users/zyh/Desktop/libSyncSDK.i386.a /Users/zyh/Desktop/libSyncSDK.arm.a -output /Users/zyh/Desktop/libSyncSDK.a
```



### lipo xxx -thin xxx -output xxx 提取支持特定CPU架构的库

发现有i386 armv7 armv7s，实际安装到真机上我们只需要armv7就可以了，我们就用lipo命令将armv7的提取出来

```
lipo LoginSDK.a -thin armv7 -output arm/LoginSDK.a
```

这样在arm文件夹中得LoginSDK.a 就是armv7架构了，大家可以用lipo -info 命令查看



### lipo -remove xxx -output xxxx 移除掉特定的cpu架构的文件

```
lipo -remove armv7 -output arm/LoginSDK.a
```

