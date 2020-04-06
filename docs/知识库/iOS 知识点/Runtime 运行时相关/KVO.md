# KVO 监听 NSObject 子类 属性变化

> Key - Value - Observer 
>
> 监听对象属性变化
>
> addObserver(forKeyPath: )

- ### 注册监听者，监听对象的 属性 变化

  ```objc
  // KVO 监听父视图的 contentOffset
  
  scrollView?.addObserver(self, forKeyPath: "contentOffset", options: .new, context: nil)
  
  // 所有 KVO 方法会统一调用此方法
  func observeValue(forKeyPath keyPath: String?, of object: Any?, change: [NSKeyValueChangeKey : Any]?, context: UnsafeMutableRawPointer?)
    
  // 移除监听者，防止内存泄漏
    superview?.removeObserver(self, forKeyPath: "contentOffset")
  ```

  