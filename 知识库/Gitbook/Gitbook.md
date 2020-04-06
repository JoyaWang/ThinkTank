# Gitbook

- 在电脑上创建一个存储 Book 的文件夹

- 初始化项目

  `gitbook init`

  > 生成 "README.md" 和  "SUMMARY.md" 两个基本文件
  >
  > - README.md
  >
  > - SUMMARY.md 总目录框架
  >
  >   > 可以在里面搭建好目录后，再 gitbook init, 会生成没有的的文件夹和文件

- 在md文件中创作

- 在本地服务器上查看电子书预览

  `gitbook serve`

  > 首先调用 `gitbook build`编译书籍，完成以后会打开一个 web 服务器，监听本地 4000 端口，在浏览器中输入`http://localhost:4000`，即可打开电子书。

- 生成电子书

  `gitbook build` 

  > 该命令会在当前文件夹中生成`_book`文件夹，里面是 html 版本的电子书

  

  ### 插件
  
  - expandable-chapters
  
    > 配置目录折叠功能如下
  
  - chapter-fold
  
    > 导航目录折叠
  
  - page-toc-button
  
    > 悬浮目录
    >
    > 貌似没起作用
  
  - back-to-top-button
  
    > 回到顶部
  
  - lightbox
  
    > 单击查看图片
  
  - custom-favicon 
  
    > 修改标题栏图标
  
  - splitter
  
    > 侧边栏宽度可调节
  
  - tbfed-pagefooter
  
    >  页面添加页脚
  
  - search-pro 
  
    > 高级搜索（支持中文）
  
  - page-treeview 
  
    > 生成页内目录
    >
    > 必须用不同的标题字体才可以，挺有用

