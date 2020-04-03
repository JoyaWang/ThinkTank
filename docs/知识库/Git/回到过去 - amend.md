# 回到过去 - amend

如果当前处于刚 commit change2.1 后的状态，想回到 change2.1 前进行修改，重新进行一次change2.1的提交

这时，直接做你要做的修改，比如，重新新建了一个文件 2.py，然后使用 `git add 2.py`  , 再使用`git commit --amend --no-edit`，这时去 git log --oneline 查看提交历史，发现最后一次提交还是 change2.1，只是前面的commit id 变了