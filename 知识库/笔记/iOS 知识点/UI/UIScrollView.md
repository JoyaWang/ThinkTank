# UIScrollView

## 使用步骤

- 添加 UIScrollView 到视图
- 设置 frame
- 设置 contentSize
- 添加 子视图 并设置 frame
- 要放大缩小的话
  - 设置 viewForZoom
  - 设置 最大、最小 缩放比

## 属性

- UIScrollView自己本身的大小，即可视区域的大小

  > frame.size

- UIScrollView中所包含的内容的大小(要滚动的实际内容的大小)

  > contentSize

- 设置UIScrollView是否能滚动

  > scrollEnabled 

- 设置分页效果是否开启，scrollView框架的大小就是每页的大小

  > pagingEnabled

- 是否允许用户交互

  > userInteractionEnabled

- 滚动偏移

  > contentOffset

- 进行偏移时有动画效果

  > setContentOffset 

- 内容内边距

  > contentInset 

- 显示水平滚动(条)指示器

  > showsHorizontalScrollIndicator

- 显示垂直滚动(条)指示器

  > showsVerticalScrollIndicator

- 设置表格滚动指示器缩进

  > scrollIndicatorInsets

- 设置UIScrollView是否有弹簧效果

  > bounces 

- 最大放大到多少倍

  > maximumZoomScale

- 最小缩放到多少倍

  > minimumZoomScale



## 常用代理协议方法

- ### 滚动

  - 滚动过程中调用

    > scrollViewDidScroll

  - 滚动停止后调用

    > scrollViewDidEndDecelerating

- ### 拖拽

  - 即将开始拖拽时调用

    > scrollViewWillBeginDragging

  - 拖拽完毕时调用

    > scrollViewDidEndDragging

- ### 放大缩小

  - 用户使用捏合手势时调用，在此返回要进行缩放的子控件，此方法在缩放之前调用

    > viewForZoomingInScrollView

  - 即将开始缩放的时候调用

    > scrollViewWillBeginZooming

  - 正在缩放的时候调用

    > scrollViewDidZoom

  - 缩放完毕的时候调用

    > scrollViewDidEndZooming

## 注意事项

1. scrollView出现在在导航控制器中，会自动加上64的偏移

   > self.automaticallyAdjustScrollViewInsets = NO;【已废弃】
   >
   > self.scrollView.contentInsetAdjustmentBehavior = UIScrollViewContentInsetAdjustmentNever;【现用】

2. ##### 设置 有导航控制器时, scrollView 不自动调整自己的原点

     **self**.edgesForExtendedLayout = UIRectEdgeNone;

     **self**.automaticallyAdjustsScrollViewInsets = **YES**;

