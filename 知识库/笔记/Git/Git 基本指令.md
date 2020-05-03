#  Git

### Git 安装

> Git 官网下载 pkg 安装

### Git 管理的文件状态

- Stage 状态【Cache】

  > 变绿了，可以被 commit 了

- Unstaged 状态

  - Unmodified

    > 刚 commit 完的状态

  - Modified

    > 上次 commit 完后，又修改了

![2-1-1](../resources/images/Git diagrams/2-1-1.png)

### 创建 Git 版本库

- 创建本地文件夹 MyProject

- 在 终端 cd 到 MyProject 文件夹

- 在 MyProject 目录下创建版本库 

  > git init
  >
  > 生成 `.git` 文件夹，意味着 MyProject 文件夹已经成为 git 管理的版本库

### 配置Git

- `git config --list` 查看 git 的完整配置信息

- `git config -l` 查看当前 git 的配置

- 设置 git 管理员信息及查看

  > - 管理员名称
  >
  >   > git config --global user.name "Joya"
  >
  > - 邮箱
  >
  >   > git config --global user.email "244092911@qq.com"
  >
  > - 查看
  >
  >   > git config user.name
  >   >
  >   > git config user.email

### 将文件交给 Git 版本库管理

> 比如在 MyProject 文件夹创建自己的文件 1.py，git status 查看当前 MyProject 版本库中文件的状态
>
> 新创建的文件必须 git add 1.py ，进入staged 转态，这样才能被 Git 管理，才能被 commit
>
> 修改了1.py 以后也要 git add 1.py ，进入 staged 状态，才能被 commit

- `git add 1.py` stage 单个文件
- `git add .` stage 所有文件(新建的或者变化了的)

### 提交更改

`git commit -m "注释"` commit 提交此次修改

`git commit -am "注释"` add 和 commit 同时进行，先 stage，后提交【适用于已经被git管理的文件】

### 查看当前 Git 状态

`git status` 查看当前 git 状态

`git status -s` short 形式显示当前 Git 状态

### 查看提交历史

`git log` 查看提交历史

`git log --oneline` 查看提交历史(每个提交显示一行, 小头版本号)

`git log --pretty=oneline`   每行显示一个commit(大头版本号)

`git log --oneline --graph` 图形显示

### 回到过去的几种方式

- amend【回到最后一次提交前修改】
- reset【commit和commit之间穿梭】
- checkout【单个文件和单个文件之间穿梭】
- rebase【将 branch B 的 commit 插入到 branch A 中】

