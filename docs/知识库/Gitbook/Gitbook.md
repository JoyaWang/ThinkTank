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

  

  