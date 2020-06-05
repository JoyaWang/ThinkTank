# gitignore

### 在项目开始时添加 gitignore 文件的步骤

- 创建项目并生成项目文件夹
- 在 git init 之前把 .gitignore 文件拖到项目文件夹【要和.git文件夹在同级文件夹】
  - 从 Github 搜索 gitignore，下载 Swift.gitignore
  - 将 Swift.gitignore 重命名为 `.gitignore`【好像是必须的】
- 在项目文件夹根目录 git init，会在此文件夹生成 .git 文件夹

```
# 从 Github 下载的默认的 gitignore 应该就是可以的了，以下这些仅做解释，不必往里面添加

#忽略所有包含xcuserdata的文件(夹)
xcuserdata 

#忽略所有以.xcuserstate结尾的文件
*.xcuserstate

#忽略所有文件夹中后缀是.DS_Store的文件
.DS_Store
```



### 如果在添加 gitignore 之前，某文件如 UserInterfaceState.xcuserstate 已被Git管理，需要做如下步骤使 gitignore 生效【试着效果不好?】

- 从被 Git 管理的文件目录中删除此文件

  > - git rm --cached `项目名`.xcodeproj/project.xcworkspace/xcuserdata/joyawang.xcuserdatad/UserInterfaceState.xcuserstate
  > - git rm -r --cached . // 删除本地缓存【貌似】

  ```
  git rm --cached CoreData\ -\ 旧.xcodeproj/project.xcworkspace/xcuserdata/joyawang.xcuserdatad/UserInterfaceState.xcuserstate
  ```

- 提交这次更改

  ```
  git commit -m "Removed file that shouldn't be tracked"
  ```

- 暂时不知有什么用

  ```
  # WARNING first try 
  git clean -f -d --dry-run, otherwise you may lose uncommited changes.
  #Then: 
  git clean -f -d
  ```

  



