# UI 界面搭建

- ### 搭建方式

  > - XIB
  > - Storyboard
  > - 纯代码
  > - SwiftUI

- ### 如何选择

  > 看界面的自定义程度，如果有许多自定义效果，定制程度比较高，就使用代码搭建。
  > 如果界面是由普通的控件组成，则用storyboard。

- ### XIB 搭建界面

  - 加载视图控制器时，如果 XIB 和 视图控制器类重名，默认构造函数会优先加载 XIB 文件

  - XIB 中拖的是 View 不是 ViewController

  - XIB 的创建

    - 当 XIB 中的 根视图是控制器的根视图时

      > - 给此 XIB 设置 视图控制器类
      >
      >   将 File's Owner 中的类设置为 XIB 的类
      >
      > - 将 视图控制器类 的 根视图 view 设置为 XIB 的 view 
      >
      >   在 File's Owner 上右键将 view 与  Xib 中的 view 连接
      >
      > - 否则会报错
      >
      >   -[UIViewController _loadViewFromNibNamed:bundle:] loaded the "JLComposeViewController" nib but the view outlet was not set.'

    - 当 XIB 中的根视图 不是控制器的根视图则不需要设置 File Owner

- ### 纯代码搭建界面

  > 直接在控制器类中自己用代码创建View，创建各种控件添加到View中，并设置frame、自动布局等