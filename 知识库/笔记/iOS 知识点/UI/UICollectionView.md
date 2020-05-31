# UICollectionView

## 使用方法

必须设置 flowLayout，必须注册 cell

- 设置 cell 的大小 flowLayout.itemSize

  > 如果设置itemSize不起作用，则将collectionView的Estimate Size设置为none

- 设置滚动的方向 flowLayout.scrollDirection

- 每行之间的最小间距 flowLayout.minimumLineSpacing

- 每个item之间的最小间距 flowLayout.minimumInteritemSpacing
- 设置分页 pagingEnabled
- 设置滚动条显示 showsHorizontalScrollIndicator
- 设置弹簧效果 bounces

- 注册 cell
  > - 从 storyboard  加载 cell
  > - 手动注册 自定义 cell 
  > - 注册 xib
  > - 注意，如果从storyboard中加载cell就不要手动注册cell了，否则cell不显示



- ### 应用

  - 新特性页面

  - 图片无限轮播功能的实现【详见网络新闻app】

    > - 始终显示第二个cell
    > - 在用户结束滑动时，通过contenOffset判断出是向上一个还是下一个滑动了
    > - 然后计算出滑动后要显示的图片的index，用全局属性currentImageIndex记录，再reloadData？
    > - 在cellForItemAt中
    > - 因为在从当前滑动到下一个图片的过程中，要开始显示下个图片了，会调用cellForRowAt，但是此时还没有滑动结束
    > - 所以新的currentImageIndex还没有计算出来，如果不在cellForItemAt中计算下个要显示的图片索引的话，下个要显示的图片将和当前相同，因为currentImageIndex没有变化。

## 注意问题

- safeArea 可能会导致 bounds 和 frame 变化，造成布局问题
- 代码添加子控件的话，添加在 contentView 中