# Stash 暂存 临时修改

- ### 场景
  - 正在 devlop 分支写代码，所以当前 git 状态为 modified 

  - 突然接到 boss 电话，master 上需要新加几行代码，因为你现在的 modified 状态，你无法切回 master，所以只能 commit 或者 stash，但你的代码还不能 commit，所以就只能 暂存 stash 了

    > - 暂存前，先 git status -s 下看看
    > - git stash 暂存
    > - 暂存完毕后，可再 git status -s 下看看

  - 然后切到 master，创建一个 boss 分支，在此分支上写上 boss 的代码，然后提交，并把 boss 合并到 master，这样 boss 的任务就完成了，删除 boss 分支。

  - 重新切回 develop ，取回暂存的代码，重新继续工作，就像一切没有发生过一样

    > - 取回暂存前，先 git status -s 下看看
    > - git stash pop 取回暂存
    > - 取回暂存后，再 git status -s 下看看

