# rebase

branchB 是主分支，branch A 是基于 branchB 的 C1 (也就是以C1为base)的，在从 c1 处创建 branchA 以后，branch 经过两次提交 C2 和 C4 修复了两个 bug，这时 branchA 也想有 C2和C4 去修改那两个bug，但是依然保留自己从创建分支一直到现在的提交 C3。相当于把 branchB 上的 C2 和 C4 插入 branch A 上的 C1 和 C3 之间。



以 rebase master 为例【危险，因为会修改 master 的 commit 历史】

- 切换到要被 rebase 的分支，比如 master

- git rebase dev

  > - branch A 指的是 从 dev 分支被创建的 那次提交 C1 开始，将 master 上的 C1 后的提交 C3 先分离出来
  > - 把 C2 和 C4 合并到 branch A【已没有C3】 上来【这时没有冲突】，把 C3 最后再拿回来，合并到 branch A 上【此时会有冲突】

- 解决冲突

  > - 冲突就是 `C2 和 C4` 与 `C3` 的冲突，解决冲突
  > - git add . 【mark them as resolved】

- 完成 rebase

  > - git rebase --continue 完成【就相当于把 dev 上的 C2 和 C4 插入到了 master 的 C1 和 C3 之间，但是**此时的 C3已非之前的 C3**， commit id 已经和之前的不同】
  >
  > - 或者
  >
  >   > git rebase --skip 【skip this commit】
  >   >
  >   > git rebase --abort 【To abort and get back to the state before "git rebase"】



![4-2-1](../resources/images/Git diagrams/4-3-1.png)

![4-3-2](../resources/images/Git diagrams/4-3-2.png)

![4-3-3](../resources/images/Git diagrams/4-3-3.png)

![4-3-4](../resources/images/Git diagrams/4-3-4.png)



![4-2-1](../resources/images/Git diagrams/4-2-1.png)