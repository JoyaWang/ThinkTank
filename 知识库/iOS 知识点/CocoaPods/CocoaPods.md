# CocoaPods

## 用CocoaPods做iOS程序的依赖管理

[用CocoaPods做iOS程序的依赖管理](http://blog.devtang.com/2014/05/25/use-cocoapod-to-manage-ios-lib-dependency/#)

[唐巧的博客](http://blog.devtang.com/)



## 安装

先安装ruby运行环境

- 查看当前 Ruby 源地址 `gem source -l`

- 添加 ruby 源 `gem sources -a https://gems.ruby-china.com`

- 两个源

  > https://rubygems.org/
  >
  > https://gems.ruby-china.com

- 设置源 `sudo gem sources -a https://ruby.taobao.org`

- 删除源 `sudo gem sources -r https://rubygems.org/`

- 删除ruby源 `gem sources --remove http://gems.ruby-china.org/` 

- 查看 ruby 版本 `ruby -v`

- 升级gem `sudo gem update --system` 

- 安装CocoaPod 

  > `sudo gem install cocoapods`
  >
  > `pod setup`
  >
  > `sudo gem install -n /usr/local/bin cocoapods`

- 更新 cocoapods `sudo gem update cocoapods` 

- 查看最新的 cocoapods 版本 `gem search cocoapods` 

- 查看当前 Cocoapods 的版本`pod --version` 

- 查看当前项目所安装的所有 Pods 的版本 `cat Podfile.lock`

  

## **管理第三方框架**

- CocoaPods使用
  - 搜索 `pod search SDWebImage`
  - 搜索`pod search afnetworking --simple`
  - 切换到项目的根目录 echo "pod 'SDWebImage'" > Podfile 【会把pod 'SDWebImage'添加到pod文件中】
  - 安装 pod install
  - 升级 pod update
  - 删除某框架 从 podfile 中删除，然后 pod install?
  - pod deintegrate

- 更新pod

  - `pod install`

    > ##### 同步其他团队成员的修改时，请使用pod install。
    >
    > 注意，pod outdated和pod update都会更新spec仓库，但是pod install不会，所以对于经常使用的pod库，建议经常pod outdated关注更新情况。

  - `pod outdated`需要更新依赖库时，先使用pod outdated查看有哪些库有更新，再使用`pod update PODNAME`有目的的更新指定库

  - `pod update PODNAME` 将某个pod库更新到最新版本时

  - `pod update`更新所有(Podfile中标明的)pods

    > 效果1：等价于对所有pod库执行一遍pod update PODNAME。
    > 效果2：若有pod库的版本发生变更，则会更新Podfile.lock文件记录当前本地库的状态。
    > 不推荐的原因是所有库只要有新版本，都会发生更新，有可能导致整个工程变得不稳定；另外，由于每个团队成员执行该命令的时间不一样，一旦中间有某个依赖库发布了新版本，这将导致团队内不同成员获得的pod库代码并不相同。

## 卸载

- 完全卸载 CocoaPods，删除其主库后重新安装【已测试，很强大，会重新下载主库，一定要使用代理】

  > `rm -rf ~/.cocoapods`
  >
  > `sudo gem install cocoapods`
  >
  > `git config --global http.https://github.com.proxy [socks5://127.0.0.1:1080](socks5://127.0.0.1:1080)`在终端为 github 设置代理

- 卸载Cocoapods 【感觉没起什么作用】

  > sudo gem uninstall cocoapods

- 更新cocoapods的主库

  > pod repo update

- 对主库进行操作，没有尝试成功！

  > pod repo remove master
  >
  > 如果没有master, 创建 repos 的 master, 并拉取
  >
  > cd ~/.cocoapods/repos/master
  >
  > git pull
  >
  > git clone --depth=1 https://github.com/CocoaPods/Specs.git

