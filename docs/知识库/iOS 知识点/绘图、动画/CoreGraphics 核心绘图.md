# CoreGraphics 核心绘图

## Quartz2D

> 二维绘图引擎，包含在 CoreGraphics 中

- ### 绘制步骤

  > 以下绘制代码写在 UIView 的 drawRect 中
  >
  > 1. 获取 图形上下文 对象
  >     CGContextRef
  >     相当于草稿纸 ，是layer类型的，和当前view的大小相同
  >     不同的上下文决定着不同的输出目标
  >     主要包含以下信息
  >     	绘图路径
  >     		(各种各样的图形)
  >     	绘图状态
  >     		(颜色、线宽、样式、旋转、缩放、平移、图片裁剪区域等)
  >     	输出目标
  >     		绘制到什么地方去？ UIView、图片、pdf文件、Bitmap或者显示器的窗口上、打印机等
  > 2. 向 图形上下文 对象中添加 路径
  > 3. 渲染 (把 图形上下文 中的图形绘制到对应的设备上)

  

- 绘制图形

  - 线条
  - 三角形
  - 矩形
  - 圆
  - 弧

- 绘制文字

- 绘制、生成图片 (图像)

- 读取、生成 PDF

- 截图、裁剪图片

- 自定义 UI 控件

  - 通过继承 UIView，重写 drawRect 方法实现在控件上绘制各种内容
  - 通过继承 UIView 实现自定义的 UIImageView
  - 实现自定义的 下载进度条 控件
  - 幸运转盘控件

- ### 实际应用

  > - 画板涂鸦
  > - 手势解锁
  > - 将矩形头像裁剪为圆形
  > - 报表
  >   - 折线图
  >   - 饼状图
  >   - 柱状图



- ### 数据类型和函数基本都以 CG 作为前缀

  ​	CGContextRef
  ​	CGPathRef
  ​	CGContextStrokePath(ctx)



## UIBezierPath

- 矩形

  +bezierPathWithRect

- 圆角矩形

  +bezierPathWithRoundedRect: radius:

- 椭圆

  +bezierPathWithOvalInRect

- 圆弧

  +bezierPathWithArcCenter

- 把笔头提到某坐标

  -moveToPoint

- 从笔头处向某坐标处添加一条线	

  -addLineToPoint

- 设置线宽	
  -setLineWidth

- 设置连接处的样式
  -setLineJoinStyle

- 设置头尾的样式

  -setLineCapStyle

- UIColor对象setStroke、setFill、set(同时设置描边和填充颜色)设置颜色

  - 描边

    -stroke

  - 填充

    -fill

  - 使用奇偶填充规则

    -useEvenOddRule

  

## 在 UIView 的 drawRect 中进行绘图

- 绘图代码为什么要写在drawRect当中

  > 因为在这个方法中可以获取到正确的上下文

- rect 参数的含义

  > 当前View的bounds

- drawRect 什么时候调用
  	
  > 这个方法是系统调用，不能手动调用！！！
  > (1)当此view第一次显示的时候调用
  > (2)当此view进行重绘redraw的时候会调用(理解成tableView的刷新)

- 如何重绘

  > 理解成tableView的刷新，当绘图的path中的坐标或其他数据改变时，如果不刷新重新显示的话，view显示的还是原来的绘图
  >
  > (1)调用某个需要重绘的view对象的setNeedsDisplay。
  >
  > (2)调用某个需要重绘的view对象的setNeedsDisplayInRect rect:参数表示需要重绘的区域

- 为什么不能手动调用drawRect

  > 因为手动调用时可能获取不到正确的上下文，画也是白画。
  >
  > 如果需要重新画一些东西的话，调用setNeedsDisplay，系统会自动在适当的时候调用drawRect

### CGRect

- offsetBy

  偏移后返回一个 Rect

- insetBy

  向内收缩后返回一个 Rect