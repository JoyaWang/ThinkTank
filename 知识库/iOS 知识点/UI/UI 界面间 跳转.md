# UI 界面间[控制器间]跳转的方式[转场]

- ### 跳转方式

  > 1. 控制器间拖线1：自动型segue
  > 2. 控制器间拖线2：手动型segue
  > 3. 纯代码：使用navigationController的push方法
  >
  > 4. Modal present

- ### 如何选择

  > - 如果两个控制器有业务关系用push，否则用modal
  > - push需要外包一个navigationController，modal不需要
  > - Modal是谁负责跳转谁负责关闭
  > - 在storyboard中，连接两个控制器时依然选show，如果有导航控制器，系统会进行push跳转，即从右往左过来，否则会modal跳转，即从下往上出来。

- ### Storyboard 控制器间拖线1：自动型segue

  > - 使用场景：
  >
  >   不需要做任何逻辑条件判断，一点就跳转
  >
  > - 步骤：
  >
  >   从A控制器要跳转的控件拖线到B控制器

- ### Storyboard 控制器间拖线2：手动型segue

  > - 使用场景：
  >
  >   点击后需要进行一些逻辑判断才能确定要不要跳转
  >
  > - 步骤：
  >
  >   * 从A控制器上面控制器图标拖线到B控制器
  >   * 给此线(segue)添加identifier
  >   * 在A控制器的类文件中合适的地方调用performSegueWithIdentifier进行跳转
  >
  > - 注意：
  >   只要是在storyboard拖线进行的跳转，无论手动还是自动型，都会调用 `prepareForSegue` 这个方法，所以可以在这里做传值、设置代理等方法。(纯代码方式不调用)

- ### 纯代码: navigationController的push

  ```swift
  // 显示
  let vc = JLDemoViewController()
  navigationController?.pushViewController(vc, animated: true)
  // 退出
  popViewController(animated: true)
  ```

  

- ### 纯代码: Modal present

  ```swift
  // 显示
  let vc = JLOAuthViewController()
  let nav = UINavigationController(rootViewController: vc)
  self.present(nav, animated: true, completion: nil)
  // 退出
  dismiss(animated: true, completion: nil)
  ```

  

