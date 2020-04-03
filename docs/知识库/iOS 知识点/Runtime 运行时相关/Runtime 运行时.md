# Runtime 运行时

- ### 利用 运行时 机制的

  - KVC
  - KVO
  - 获取属性列表、成员变量列表和方法列表
  - 反射机制
  - 注册监听通知
  - 监听点击事件
  - 代理模式？

- ### 注册监听通知

  > 实例应用 QQ聊天

  - 特点

    > - 一对多，可以有多个监听者监听事件，只要有注册的监听者，在注销监听之前，都可以接收到通知！
    > - 发生事件时，将通知发送给通知中心，通知中心再`广播`通知！，效率相对代理较低
    > - 如果层次嵌套太深，可以使用通知传值

  - 使用

    ```swift
    // 发布通知
    NotificationCenter.default.post(name:Notification.Name.init(rawValue:JLUserShouldLoginNotification), object: "bad token")
    // 注册监听通知
    NotificationCenter.default.addObserver(self, selector: #selector(userLogin), name: NSNotification.Name(rawValue: JLUserShouldLoginNotification), object: nil)
    // 移除通知，防止内存泄漏
    NotificationCenter.default.removeObserver(self)
    ```

- ### 代理模式

  - 特点

    > - 一对一，只能有一个监听者监听事件，最后一个设置的代理对象有效！
    > - 发生事件时，直接让代理执行协议方法，效率更高
    > - 直接反向传值
    > - 如果层次嵌套太深，不利于传值，可以使用通知传值

- ### 监听点击事件

```swift
btn.addTarget(self, action: #selector(buttonTapped(_:)), for: .touchUpInside)
```

