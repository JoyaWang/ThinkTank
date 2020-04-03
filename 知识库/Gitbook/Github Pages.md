# Github Pages

GitHub Pages 的静态资源支持下面 3 个来源：

- - master 分支
  - master 分支的 /docs 目录
  - gh-pages 分支



- 第一种方式

  在生成静态网页时，将保存的目录指定为 ./docs【gitbook build会替换原来的_book文件夹，所以每次生成到./docs文件夹，让gitpages从那加载】

  > ```
  > $ gitbook build ./ ./docs
  > ```

  然后直接推送到 GitHub 仓库的

  > ```
  > $ git push origin master
  > ```

- 第二种方式

  执行下面命令，将 _book 目录推送到 GitHub 仓库的 gh-pages 分支。【gitbook build会替换原来的_book文件夹，所以每次上传的时候，也用最新的_books文件夹完全覆盖gh-pages】

  > ```
  > $ git subtree push --prefix=_book origin gh-pages
  > ```







