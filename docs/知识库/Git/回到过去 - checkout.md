# 回到过去 - checkout

> 【单个文件和单个文件之间穿梭】

- git checkout `要回到的commit id` -- `单个文件`

  > git checkout 3a2fc25 -- 1.py
  >
  > 将 1.py 文件穿梭到了 3a2fc25 这次刚 commit 后的时代，而 3a2fc25 到未来最后一次 commit 之间的数据就没有了呢！
  >
  > 然后在那里进行修改，修改完后 add，再 commit，这样就又重新回到了未来，这时 1.py 就保持了此次 commit 后的状态，其它的文件都处于未来没有变

- checkout 还可以在 branch 分支 之间来回穿梭