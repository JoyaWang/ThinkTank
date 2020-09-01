# 打Tag标签

- 列出本地标签

  > git tag --list

- 给当前head打Tag标签

  > git tag `Handling_User_Input`   Handling_User_Input 是标签

  > git tag -m `'新发布1.0.1'` `1.0.1`   -m后面是备注 1.0.1才是标签

- 给某次提交commit打标签Tag

  > git tag -a `Building_Lists_and_Navigation` 9fbc3d0

- 删除标签tag 

  - 删除本地仓库的标签tag
  
    > git tag -d `Building_Lists_and_Navigation`
  
  - 删除远程仓库的标签tag
  
    > git push origin :refs/tags/v1.0.1
  
- 推送本地标签 tag 到远程仓库

  > git push origin Handling_User_Input
  >
  > git push --tags