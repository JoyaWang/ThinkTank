# UIView 和 CALayer

## UIView

- 负责监听和响应事件

- ### 圆角相关

  - 圆角 layer.cornerRadius
  - 圆角以后非圆角的地方截掉 layer.masksToBounds 

- ### 布局子控件大小、位置

  - frame

    > 控件所在矩形框在其父控件中的位置和尺寸
    >
    > 以父控件的左上角为坐标原点
    >
    > frame.origin即可修改控件位置，就修改它的frame的左上角的位置坐标
    >
    > frame.size又可修改控件大小，修改它的frame的矩形的长宽(左上角左边不变，中心点会变化)

  - bounds

    > 控件所在矩形框的位置和尺寸 bounds.size只可以修改控件大小，放大尺寸时，中心点不变

  - center

    > 控件中点的位置（以父控件的左上角为坐标原点）
    >
    > 可以通过center的坐标改变控件的位置

  - -sizeToFit

    > (command + =) 根据里面的内容设置自己UIView适应大小，不改变x,y

  - setNeedsLayout

  - layoutIfNeeded

    > 每调用一次，系统会立即在绘图之前进行一次自动布局，比如当cell刚创建好时，我们在layoutSubview里面的code之前需要对某子控件先进行布局，得到它合适的尺寸之后才能进行code的布局，就可以这样

  - layoutSubviews 

    > (在layoutIfNeeded中调用)当控件的frame改变时会调用，怎样重新布局它的子控件，需要重写此方法，在此方法中规定如何根据父控件的frame计算子控件的frame。

- ### 绘图相关

  - setNeedsDisplay

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

- ### 坐标转换

  - 将自己的子控件的坐标，转换为另一个视图的坐标 convert 

- ### 动画相关

  - view.transform 

    > (transform是个结构体类型)控件的形变属性(可设置旋转角度、比例缩放、平移等属性)
    >
    > 平移 CGAffineTransformTranslation
    >
    > 缩放 CGAffineTransformScale
    >
    > 旋转 CGAffineTransformRotation

  - 动画开始的地方 +beginAnimations context

  - 设置动画持续时间 +setAnimationDuration 

  - 提交动画(动画结束的地方) +commitAnimations

  - 形式使用动画 +animateWithDuration: animation block

- ### 视图生命周期相关

  - init?(coder: NSCoder) 从 XIB，Storyboard 加载时的构造函数

    > 只是刚从 XIB 的二进制文件将视图数据加载完成，还没有和代码连线建立起关系，所以开发时不能在此处理 UI，控件还是 nil

  - init(frame:) 纯代码创建视图的入口 

  - awakeFromNib

    > 在这里处理 UI, UIView从xib文件中创建好时会自动调用这个方法，这个时候这个view的子控件也都创建好可以访问了

  - willMoveToSuperview:newSuperview; 

    > addSubview 时会调用 willMove
    >
    > - 当添加到父视图的时候， newSuperview 是 父视图
    >
    > - 当父视图被移除，newSuperview 是 nil

  - didMoveToSuperview;

  - willMoveToWindow:newWindow;

    > 当视图从界面上删除，同样会调用此方法， newWindow == nil

  - didMoveToWindow;

  - removeFromSuperview

  - viewWithTag

- ### 其他

  - viewWithTag 返回对应tag标识的子控件
  - bringSubviewToFront 将此子控件放置到所有子控件的最上方(若某个子控件被挡住无法显示)

## CALayer

> CALayer负责视图中显示内容和动画
>
> UIView负责监听和响应事件
>
> UIView之所以能够显示在屏幕上，完全是因为它内部的一个图层
>
> 在创建UIView对象时，UIView内部会自动创建一个图层(即CALayer对象)，通过UIView的layer属性可以访问这个层
>
> 当UIView需要显示到屏幕上时，会调用drawRect方法进行绘图，并且会将所有内容绘制在自己的图层上，绘制完毕后，系统会将图层拷贝到屏幕上，于是就完成了UIView的显示。
>
> 也就是说，UIView本身不具备现实的功能，是它的内部的层才有显示功能
>
> CoreAnimation动画是直接作用在CALayer上的，并非UIView



- position 

  > 用来设置在父层中的位置
  >
  > 以父层的左上角为原点(0,0)
  >
  > position属性和view.center的关系

- anchorPoint

  > 称为”定位点“、”锚点“
  >
  > 决定着CALayer的position属性所指的是哪个点
  >
  > 以自己的左上角为原点(0,0)
  >
  > 它的x, y取值范围都是0~1，默认值为(0.5, 0.5)

- contents设置内容(图片)

  > 需要桥接bridge，__bridge后面直接跟要从C转为OC的类，比如id，就用(__bridge id)
  >
  > 获取图片

- 圆角 cornerRadius

- 形变 transform

- 阴影

  - 阴影颜色 shadowColor
  - 阴影透明度? shadowOpacity
  - 从要加阴影的控件的左上角偏移的量 shadowOffset 
  - 阴影半径? shadowRadius