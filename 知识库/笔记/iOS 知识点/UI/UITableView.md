# UITableView

## 实例应用

- 网络新闻_新闻列表_
- _UI基础_汽车品牌展示
- UI基础_团购案例_
- 彩票_设置界面

## UITableViewController

- 表格种类

  > UITableViewStylePlain 在上拉的时候，把组头顶在顶部。
  >
  > UITableViewStyleGrouped 每个 section 之间有间距

- 单元格种类

  > dynamic 动态：数量可以根据数组元素的数量动态变化，样式可以变化
  >
  > static 静态：数量固定，样式固定？
  >
  > 使用静态单元格，必须使用UITableViewController控制器



在控制器中需设置自定cell的高度，因为tableView继承自UIScrollView，所以必须知道自己的contentSize来确定可滚多远，它要通过每个cell的高度来计算

- ### 背景色相关

  - 设置整个表的背景色 tableView.backgroundColor 
  - 设置单元格的背景颜色 cell.backgroundColor
  - 设置单元格的背景视图 cell.backgroundView

- ### 高度相关

  - 统一设置整个表所有单元格的高度 tableView.rowHeight 【每行 行高相同时】

  - 统一设置整个表所有组标题的高度 tableView.sectionHeaderHeight

  - 统一设置整个表所有组尾的高度 tableView.sectionFooterHeight 

  - **动态设置每个单元格的行高** heightForRowAtIndexPath 【Delegate方法，每行行高不同时】

    > - 动态设置行的高度（代理协议中的方法），根据单元格中最底下的控件的maxY和margin计算出行高
    > - heightForRowAtIndexPath比cellForRowAtIndexPath中的layoutSubviews提前调用，也就意味着那时根据子控件的frame计算行高就晚了，所以行高必须在heightForRowAtIndexPath调用之前计算，可以将这个数据作为model的一个属性储存在model中。
    > - 在Table View Cell 的尺寸检查器中设置的Row Height只是改变了storyboard里面的cell的高度，程序实际运行起来以后，如果不在tableView.rowHeight或者heightForRowAtIndexPath中设置行高的话，则会使用系统的默认行高。

- ### 分割线相关

  - 分割线的颜色 tableView.separatorColor 
  - 分割线的样式 tableView.separatorStyle 
  - 分割线的内边距 [tableView setSeparatorInset]; 
  - 没有数据时不显示tableView的分割线 _tableView.tableFooterView = [[UIView alloc]initWithFrame:CGRectZero];

- ### content相关

  - 设置表格内容缩进，即内容内边距 contentInset
  - 设置内容偏移 - 滚动到表格视图某个位置【最顶部】  [tableView setContentOffset];	

- ### 表头表尾，组头组尾相关

  - 表头，一般可以放广告  tableView.tableHeaderView
  - 表尾，一般可以放加载更多 tableView.tableFooterView
  - 组标题显示文字 titleForHeaderInSection 【dataSource】
  - 组尾/脚显示文字(组描述) titleForFooterInSection 【dataSource】
  - 组标题显示view，可以是任何控件 viewForHeaderInSection【dataSource】
  - 组尾显示view，可以是任何控件 viewForFooterInSection【dataSource】

- ### 选中单元格

  - 是否允许单元格被选中 tableView.allowSelection
  - 监听单元格被选中事件的方法 didSelectRowAtIndexPath【Delegate】
  - 监听单元格取消选中事件的方法 didDeselectRowAtIndexPath【Delegate】
  - 获取被选中(点击)cell的位置(indexPath) tableView.indexPathForSelectedRow 
  - 设置选中cell时的样式，可取消灰色 cell.selectionStyle
  - 设置选中单元格时要展示的view，也可设置颜色 cell.selectedBackgroundView

- ### 刷新表格

  - 刷新整个列表 [tableView reloadData] 
  - 刷新指定的组 [tableView reloadSections];
  - 刷新指定的行 [tableView reloadRowsAtIndexPaths] 当数据总行数发生变化时不能使用

- ### 滚动

  - 将tableView滚到指定的某行 [tableView scrollToRowAtIndexPath]
  - 设置表格滚动指示器缩进 tableView.scrollIndicatorInsets

- ### 单元格样式

  - styleDefault 左边一张图、一个标题
  - styleSubtitle 左边一张图、一个标题，标题下面一个副标题
  - styleValue1 左边一张图、一个标题，右边一个副标题
  - styleValue2 一个标题和一个副标题紧挨着

- ### 创建单元格

  - #### Xib

    - 创建 与 自定义Cell 类名 相同的 Xib 文件

      > 添加控件，在 Xib 中做好自动布局，宽度和高度需要动态变化的 label，固定好Leading、Trialling，设置动态 trailing 和 bottom，label trailing 小于等于 Cell Trailing, 可设 constant 来设置与Cell Trailing 的间距 

    - 设置 Xib 文件的 class 为 自定义类

    - 将 Xib 控件连线到自定义类

    - 注册 Xib cell class

      > 必须使用 tableView.register(nib,forIndexPath)

    - 创建 Xib cell 实例

      > 直接 tableView.dequeReusableCell (withIdentifier forIndexPath) as! XibCellClass

    - Xib Cell 好像不用再显式设置 cell 的高度了，就已经是动态高度了。

      > 如果需要显式设置的话，设置这俩 tableView?.rowHeight = UITableView.automaticDimension，tableView?.estimatedRowHeight = 300

  - #### Storyboard

  - #### 纯代码

- ### 单元格编辑模式左滑、右滑、删除

  - 进入编辑模式 commitEditingStyle: forRowAtIndexPath: 【Delegate】
  - 删除指定行的单元格 deleteRowsAtIndexPaths: withRowAnimation:【Delegate】
  - 右滑单元格出现的按钮定制 leadingSwipeActionsConfigurationForRowAtIndexPath
  - 左滑单元格出现的按钮定制 trailingSwipeActionsConfigurationForRowAtIndexPath

- ### 单元格重用

  > 1. 声明一个重用ID
  >
  >    static 后，ID局部变量就不会每次重复创建重复销毁了，一旦创建就会一直保留直到程序结束 
  >
  > 2. 根据这个重用ID去“缓存池”中查找对应的cell
  >
  > 3. 判断是否找到了可用的cell，如果没有，则需要重新创建一个(如果使用tableView自带的cell，设置reuse identifier后就不需要判断和创建了，storyboard自动做这些工作)

- ### 标题、文字、图片相关
  - 图片框 cell.imageView

  - 大文字标签 cell.textLabel			

  - 小文字标签 cell.detailTextLabel	

  - 列表右侧的索引栏，目录 sectionIndexTitlesForTableView 		

  - 单元格右边的小控件枚举 (disclosureIndicator, detailDisclosure)

    > - cell.accessaryType
    > - cell.accessoryView

## 常见问题

- 代码添加子控件的话，添加在 contentView 中
- 滚动到表格视图最顶部 setContentOffset

## 表格的性能优化

- 尽量少计算，所有需要的素材提前计算好！
- 控件上不要设置圆角半径，所有图像渲染的属性，都要注意！
- 图像尺寸不合适时进行的拉伸要避免，用 CoreGraphics 画
- 不要动态创建控件，所有需要的控件，都要提前创建好，在显示的时候，根据数据 隐藏 / 显示！
- Cell 中的控件的层次越少越好，数量越少越好！
- 用内存换取 CPU
- 要测量，不要猜测

