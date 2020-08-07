# 打Tag标签

- 给当前head打Tag

  > git tag `Handling_User_Input`   Handling_User_Input 是标签

  > git tag -m `'新发布1.0.1'` `1.0.1`   -m后面是备注 1.0.1才是标签

- 给某次commit打Tag

  > git tag -a `Building_Lists_and_Navigation` 9fbc3d0

- 删除tag 

  > git tag -d `Building_Lists_and_Navigation`
  
- 推送 tag 到远程仓库

  > git push origin Handling_User_Input
  >
  > git push --tags