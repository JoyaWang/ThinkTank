# 分支及合并 branch & merge

### 查看所有分支，以及当前所在的分支

`git branch` 

### 创建分支

> 【从当前分支，可以是任一分支】创建名为 dev 的分支

`git branch dev`

### 切换分支

> 切换到 dev 分支，将 HEAD 指针放到 dev 分支

`git checkout dev`  

### 删除分支

> 删除 dev 分支【只有当前HEAD不在dev分支时才起作用】

`git branch -d dev`

`git branch -D boss`

### 创建分支的同时切换分支

> 【从当前分支，可以是任一分支】创建 dev 分支的同时，切换到 dev 分支 (即将 HEAD 指针放到dev分支)

`git checkout -b dev` 

### 合并分支

- 先切回主分支 `git checkout master`

- git merge dev` 

  > 使用 fast forward 方式合并 dev 分支到 master 分支，不添加这次合并的注释信息

- `git merge --no-ff -m "合并dev到master" dev`

  > 合并分支，不使用 fast forward 的方式，会添加这次合并的注释。如果 dev 和 master 没有冲突的话就直接成功了

### 解决合并过程中的冲突

> 创建了 dev 后，你在 dev 上修改，但同时有人在 master 上修改，当你合并时，就会出现冲突，这时需要解决冲突，解决完了以后，<u>**切记！！！要 add 和 commit 一次**</u>，注释为 `解决冲突` ，因为解决冲突后处于 modified 状态的，提交后就算合并成功了
>
> 解决冲突合并后，并不意味着 master 和 dev 的所有都一样了？，master 上会比 dev 多出 `修改了但没有和 dev 冲突的部分`?
>
> 将 dev 与 master 合并了一次以后，如果 dev 再不更改，即便 master 更改了，再次合并 dev ，也无法合并，会显示 "already up to date"

 





 

