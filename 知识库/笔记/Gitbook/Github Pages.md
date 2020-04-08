# Github Pages

> Github Pages 功能介绍
>
> 首先，必须在 Github 创建一个 `joyawang.github.io` 为名的仓库(Repository)【只能创建一个?】用来当做Github Pages https://joyawang.github.io/ 的主页
>
> 在此仓库的设置界面找到 Github Pages 选项， 就可以设置主页的网页内容来源了，默认从此仓库的 master 分支加载 index.html 文件
>
> 从现在开始，Github 任何一个仓库都可以在 https://joyawang.github.io/ 上托管页面
>
> 在 Github 创建一个 ThinkTank 仓库，在设置界面找到 Github Pages，将来源选为 master 分支的 /docs 文件夹【也可选其他方式】
>
> 这样，https://joyawang.github.io/ThinkTank 就会从 ThinkTank 仓库 master 分支的 docs 文件夹加载 index.html 文件。
>
> 所以，只要将你生成的书的 html 文件实时上传到 ThinkTank 仓库 master 分支的 docs 文件夹，你就可以从 https://joyawang.github.io/ThinkTank 访问你的书内容了



GitHub Pages 的静态资源支持下面 3 个来源：

- - master 分支
  - master 分支的 /docs 目录
  - gh-pages 分支



- 第一种方式

  - 在生成静态网页时，将保存的目录指定为 ./docs【gitbook build会替换原来的_book文件夹，所以每次生成到./docs文件夹，让gitpages从那加载】

    `$ gitbook build ./ ./docs`

  - 然后 `git add .` 并且 `git commit` 提交

  - 最后推送到 GitHub 仓库，更新 master 上的 /docs 文件夹中的内容

    `$ git push origin master`

- 第二种方式

  执行下面命令，将 _book 目录推送到 GitHub 仓库的 gh-pages 分支。【gitbook build会替换原来的_book文件夹，所以每次上传的时候，也用最新的_books文件夹完全覆盖gh-pages】

  > ```
  > $ git subtree push --prefix=_book origin gh-pages
  > ```







