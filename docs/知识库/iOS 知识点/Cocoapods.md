# Cocoapods 

### **管理第三方框架**

- 安装
  - 查看源 gem source -l
  - 设置源 sudo gem sources -a https://ruby.taobao.org
  - 删除源 sudo gem sources -r https://rubygems.org/
  - 安装CocoaPod sudo gem install cocoapods

- CocoaPods使用
  - 搜索 pod search SDWebImage
  - 切换到项目的根目录 echo "pod 'SDWebImage'" > Podfile 【会把pod 'SDWebImage'添加到pod文件中】
  - 安装 pod install
  - 升级 pod update
  - 删除某框架 从 podfile 中删除，然后 pod install?
  - pod deintegrate

### 发布框架

- 注册

```
pod trunk register xxx@gmail.com "我的名字"
```

- 查询 pod 注册信息

```
pod trunk me
```

- 生成 spec 文件

```
pod spec create https://github.com/liufan321/FFFirst
```

- 编辑 `podspec` 文件

![Screen Shot 2020-03-23 at 2.16.11 PM](/Users/joyawang/Library/Application Support/typora-user-images/Screen Shot 2020-03-23 at 2.16.11 PM.png)

- 验证  spec 文件

```
pod spec lint

pod spec lint --verbose
```

- 推送

```
pod trunk push
```

