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

    - 加载控制器

      ```objc
      +(instancetype)viewControllerFromXib {
          
          return [[JLRecoverPwdViewController alloc] initWithNibName:@"JLRecoverPwdViewController" bundle:[NSBundle mainBundle]];
      }
      ```
      
    - 加载 View
    
      ```objc
      + (instancetype)rotationView {
        return [[NSBundle mainBundle] loadNibNamed:@"JLTopImageRotationView" owner:nil options:nil][0];
      }
      ```
      
      
      
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
    
    - 如果 Xib 文件对应的是 view， 不是 控制器，那么 fileOwner 不需要设置
    
    - Xib 中的 collectionView 不像 Storyboard 中一样，不能添加 item，创建自定义 UICollectionViewCell
    
    - 如果 collectionView 的superView 是从 Xib 中加载的，设置 itemSize 和 superView 相关的话，要在 layoutSubviews 中设置，因为 awakeFromNib 中 superView 的 size 还是 xib 中的size
    
    - 创建 Cocoa Touch 类时，只有 Controller 的子类，可以直接自动创建 Xib，view 则不行

- ### 纯代码搭建界面

  > 直接在控制器类中自己用代码创建View，创建各种控件添加到View中，并设置frame、自动布局等