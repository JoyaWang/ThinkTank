# Swift函数

## 目标

- 函数
  - 定义格式
  - 外部参数
  - 函数的默认值
  - 无返回值的三种情况
- 闭包
  - 闭包的定义
  - 尾随闭包
  - 循环引用以及接触循环引用的方法
- GCD在Swift中的写法

```swift
    func loadData(completion: @escaping (_ result:[String])->()) {
        DispatchQueue.global().async {
            print("耗时操作 \(Thread.current)")
            // 休眠，模拟网络耗时
            Thread.sleep(forTimeInterval: 1.5)
            // 获取网络json数据
            let json = ["新闻","曝光","军事"]
            // 回到主线程更新UI控件，通过回调的方式
            DispatchQueue.main.async {
                completion(json)
            }
        }
    }
```

