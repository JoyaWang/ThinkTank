# UINavigationController 

### Navigation Controller

负责跳转
	push
	pop
避免系统的覆盖，需要隐藏默认的 Bar
	两种隐藏方式
		一个支持手势返回
		一个不支持
需要在每个子控制器添加 Bar



### NavigationBar

​	一个控制器只有一个
​	bar 的背景颜色
​		bar.barTintColor
​	负责管理 NavigationItem
​	手势返回的时候，前后的导航条会覆盖
​	可以自定义 NavigationBar 解决融合？



### NavigationItem

​	管理条目
​		中间的标题
​			标题字体颜色
​				bar.titleTextAttributes
​		左侧按钮
​		右侧按钮
​		返回按钮

### UIBarButtonItem

​	具体的按钮
​	按钮标题字体颜色
​		bar.tintColor



### 导航栏颜色相关

```
// 设置导航栏的 背景颜色【渲染颜色】
navigationBar.barTintColor = UIColor.cz_color(withHex: 0xF6F6F6)

// 设置导航栏 标题的字体颜色
navigationBar.titleTextAttributes = [NSAttributedString.Key.foregroundColor : UIColor.darkGray]

// 设置导航栏 按钮文字颜色
navigationBar.tintColor = UIColor.orange
```

导航栏底部隐藏线条 [[UINavigationBar appearance] setShadowImage:[[UIImage alloc] init]];

### 设置 有导航控制器时, scrollView 不自动调整自己的原点

  **self**.edgesForExtendedLayout = UIRectEdgeNone;

  **self**.automaticallyAdjustsScrollViewInsets = **YES**;