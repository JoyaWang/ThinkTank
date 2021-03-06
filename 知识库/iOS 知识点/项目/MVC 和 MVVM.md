

## MVVM

MVVM 是 Model-View-ViewModel 的简写，MVVM 和 MVC 一样，主要目的是分离视图 (View) 和模型 (Model)



用一个 viewModel 为整个视图中所有控件提供数据，控制器只负责刷新一下就行，大大减少了控制器中的代码

V  视图【View + Controller】



- VM  视图模型【viewModel】
  - 字典转模型
    - 加载数据【调用 JLNetworkTool 方法】
  - 下拉刷新
  - 上拉刷新

M 数据模型【Model】

### MVC 回顾

![MVC](../../images/MVC.png)

- MVC 存在的问题
  - 模型的代码很少
  - 控制器的代码一不小心就越来越多
  - 不好测试

### MVVM

- MVVM 结构图

  ![MVVM](../../images/MVVM.png)

- MVVM 概念
  - 在 MVVM 中，view 和 view controller 正式联系在一起，我们把它们视为一个组件
  - view 和 view controller 都不能直接引用 model，而是引用视图模型
  - view model 是一个放置用户输入验证逻辑，视图显示逻辑，发起网络请求和其他代码
- MVVM 使用事项
  - view 引用 view model ，但反过来不行
  - view model 引用了 model，但反过来不行
  - 如果破坏了这些规则，便无法正确的使用 MVVM

### MVVM 的优点

- 低耦合: View 可以独立于 model 变化和修改，一个 ViewModel 可以绑定到不同的 View上
- 可重用性: 可以把一些试图逻辑放在一个 ViewModel 里，让很多 view 重用这段视图逻辑
- 独立开发: 开发人员可以专注于业务逻辑和数据开发 ViewModel，设计人员可以专注于页面设计
- 可测试: 通常界面是比较难于测试的，而 MVVM 模式可以针对 ViewModel 来进行测试

