# UIDevice

> 如何监听设备旋转、电池电量改变、贴近脸部(近距离传感器)等事件？

> UIDevice类提供了一个单例对象，它代表着设备，通过它可以获得一些设备相关的信息，比如电池电量值(batteryLevel)、电池状态(batteryState)、设备的类型(model, 比如iPod、iPhone等)、设备的系统(systemVersion)

UIDevice对象会不断地发布一些通知，下列是UIDevice对象所发布通知的名称常量：
设备旋转 UIDeviceOrientationDidChangeNotification

- 电池状态改变 UIDeviceBatteryStateDidChangeNotification 
- 电池电量改变 UIDeviceBatteryLevelDidChangeNotification
- 近距离传感器(比如设备贴近了使用者的脸部) UIDeviceProximityStateDidChangeNotification 

```objc
UIDevice *dev = [UIDevice currentDevice];
NSNotificationCenter *center = [NSNotificationCenter defaulterCenter];
[center addObserver:self selector:@selector(m1:) name:UIDeviceOrientationDidChangeNotification object:dev];
```

