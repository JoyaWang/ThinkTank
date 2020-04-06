# 回到过去 - reset

> 【在 commit 和 commit 之间来回穿梭】



- 当前处于修改了 1.py ，刚 git add 1.py 后的 staged 状态，还没有 commit，但是我后悔刚才 git add 了，不想过早地处于 stage 状态，想返回到 staged 前的 modified 状态去继续进行修改。

  > 使用 git reset 1.py ，就重新回到 modified unstaged 状态了，相当于之前没有 git add 1.py

- 当前还处于上述`当前处于修改了 1.py ，刚 git add 1.py 后的 staged 状态，还没有 commit，但是我后悔刚才 git add 了，不想过早地处于 stage 状态，想返回到 staged 前的 modified 状态去继续进行修改` 状态，我可以用 `git reset --hard HEAD` 回到最后一次 commit 后的 clean 状态，相当于最后一次 change 2.1 的提交后，我啥都没干，即舍弃了从那之后的所有更改

  > HEAD 指针在哪，当前文件夹中的文件就处于哪个时代，意味着我们就可以在哪个时代进行编辑和修改，master 指的是
  >
  > git reset --hard HEAD 就相当于回到了上次提交后的状态，从那之后我啥都没干

- git reset --hard HEAD

  - `git reset --hard HEAD`

    > 回到最后一次(上一次)提交，将 HEAD 指针放到最后一次 commit id 的头顶，当前文件夹中的文件处于刚进行了最后一次 commit 后的时代，从那时起啥都没弄

  - `git reset --hard HEAD^`

    > 回到倒数第二次(上上次)提交

  - `git reset --hard HEAD^^`  或者`git reset --hard HEAD~2`

    > 回到倒数第三次(上上上次)提交

- `git reset --hard 4077e4e` 即使用 commit id

  > 回到 commit id 那一次刚提交后的状态

- 通过 reset 回到过去某次提交`3edb`后，git log --oneline 就会发现`3edb`提交后的所有提交都不见了

- 这时如果想又回到未来，需要使用 `git reflog` 通过查看每一步 HEAD 的移动变化，找到未来的那次提交的 commit id， 在通过 `git reset --hard commitid` 的方法回到未来。

![2-2-1](../resources/images/Git diagrams/2-2-1.png)

![2-2-2](../resources/images/Git diagrams/2-2-2.png)

![2-2-3](../resources/images/Git diagrams/2-2-3.png)

![2-2-4](../resources/images/Git diagrams/2-2-4.png)
