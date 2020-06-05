## 重写setter方法



```swift
// 模型 -> 给视图设置模型，由视图自己根据模型的数据，决定显示内容
    var person:Person? {
        // *** 就是替代 OC 中重写 setter 方法
        // 区别: 再也不需要考虑 _成员变量 = 值!
        // OC 中如果是 copy 属性，应该 _成员变量 = 值.copy; 容易忘记
        didSet {
            text = person?.name
        }
    }
```

