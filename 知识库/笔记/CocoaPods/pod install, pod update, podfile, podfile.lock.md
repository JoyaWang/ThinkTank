# pod install, pod update, podfile, podfile.lock, 版本号控制

# 一、pod install VS pod update

### 1  pod install 的使用场景：

- 1.1 新创建工程，第一次引入pod库时。

  > 效果1：此时会按照Podfile中给出的约束条件下载所需要的pod库，获得符合约束条件的最新版本。
  >  效果2：将创建Podfile.lock文件，记录当前使用的所有pod库和版本。
  >  效果3：同时也会创建Pods.xcodeproj和.xcworkspace，不过这不是主要功能。

- 1.2 修改了Podfile文件，添加或删除了所依赖的pod库时。

  > 效果1：建议此时一定要使用pod install获取新的pod库或删除不要的pod库，若使用pod update其他库也会受到影响。
  >  效果2：Podfile.lock会做相应的修改，记录当前使用的所有pod库和版本。
  >  效果3：对于Podfile.lock中已有记录的其他pod库不会发生任何变化，不去检查是否有更新版本，即使有新的可用版本也不会更新。

- 1.3 新人加入团队，拉取了主工程之后要获取pod库时。

  > 效果1：按照Podfile文件中的依赖关系获取pod库。
  >  效果2：在满足Podfile文件的情况下，直接获取Podfile.lock中记录的pod库的对应版本，并不去检查是否有更新版本。因此，即使有新的可用版本也会仅获取Podfile.lock中的版本。

- 1.4 团队合作中，不同开发者之间要同步对pod库的依赖时。

  > 效果1：有人改变依赖关系，修改了Podfile文件时，情况与见场景2相同。
  >  效果2：Podfile文件未变化，但是有人执行了pod update导致Podfile.lock文件发生修改时，pod install会同步获取Podfile.lock中指定的pod库版本，而不是最新的版本。
  >
  > 效果3：如果Podfile与Podfile.lock的记述相冲突，如指定了低于Podfile.lock中记录的版本，会以Podfile为准，并在获取完成后更新Podfile.lock文件。

  

### 2 pod update 的使用场景：

- 2.1 需要将某个pod库更新到最新版本时，使用pod update PODNAME

  > 效果1：检查指定pod库的最新版本，若最新版本满足Podfile中的约束，则更新到最新版本。
  >  效果2：若最新版本不满足Podfile中的约束，则更新到满足约束的最高版本。
  >  效果3：pod update命令不会检查Podfile.lock文件，即使其中有记录也是无效的。
  >  效果4：若Podfile文件已发生变更，pod update命令也会将本地pod库更新为符合Podfile文件的版本（不建议这么做，因为非指定PODNAME的pod库也可能被改动，此处仅写明有此效果而已）。
  >  效果5：若有pod库的版本发生变更，指定pod库版本变化、其他pod库由于Podfile的改动而发生变化、甚至因为Podfile的改动而被移除，都会更新Podfile.lock文件记录当前本地库的状态。
  >  效果6：由于要检查pod库的新版本，会先拉取所有源的podspec文件，第一次做这件事将是个超级费时的操作。

- 2.2 超级懒人爱做，而官网极其不推荐的做法，直接使用pod update

  > 效果1：等价于对所有pod库执行一遍pod update PODNAME。
  >  效果2：若有pod库的版本发生变更，则会更新Podfile.lock文件记录当前本地库的状态。
  >  不推荐的原因是所有库只要有新版本，都会发生更新，有可能导致整个工程变得不稳定；另外，由于每个团队成员执行该命令的时间不一样，一旦中间有某个依赖库发布了新版本，这将导致团队内不同成员获得的pod库代码并不相同。

### 3 正确的使用方法

根据这两个命令的功能差异，以及CocoaPods官网的建议，我总结它们的正确用法是：

1. 第一次获取pod库时，应使用pod install。
2. 需要更新依赖库时，先使用pod outdated查看有哪些库有更新，再使用pod update PODNAME有目的的更新指定库。
3. 提交代码时，请注意一定同时提交Podfile.lock文件，以便其他人能同步到与你相同的pod库版本。
4. 同步其他团队成员的修改时，请使用pod install。

注意，pod outdated和pod update都会更新spec仓库，但是pod install不会，所以对于经常使用的pod库，建议经常pod outdated关注更新情况。

------

官网提到的：为什么直接在Podfile文件中指定版本的方法不够用？

原因是你所依赖的库可能还依赖于其他的库。

如果指定pod A的版本（如在Podfile中指定pod 'A', '1.0.0'），但是pod A依赖于pod A2（通过在A.podspec中的dependency 'A2', '~> 3.0'声明）。在这种情况下，Podfile的确会强制所有用户使用pod A的1.0.0版本，但是，用户1可能会使用A2的3.4版本，而在这之后A2有新版发布，若无Podfile.lock的帮助，用户2无论使用pod install还是pod update都不可避免的会使用A2的3.5版本。

一般情况下pod A对pod A2依赖关系你是不可见的，或者并不由你维护的。所以，直接在Podfile文件中指定版本的方法并不能保证所有用户都使用相同版本的pod库。

除非你的工程所依赖的所有pod库在对其他库进行依赖时也都采用指定版本的方法，而这只有在所有pod库都由你来维护时才能够得到保证。

# 二、对于版本号的控制

pod ‘AFNetworking’ //不指定依赖库版本，表示每次都获取最新版本
 pod ‘AFNetworking’, ‘2.0’ //只使用2.0版本
 pod ‘AFNetworking’, ‘> 2.0’ //使用高于2.0的版本
 pod ‘AFNetworking’, ‘>= 2.0’ //使用大于或等于2.0的版本
 pod ‘AFNetworking’, ‘< 2.0’ //使用小于2.0的版本
 pod ‘AFNetworking’, ‘<= 2.0’ //使用小于或等于2.0的版本
 pod ‘AFNetworking’, ‘~> 0.1.2’ //使用大于等于0.1.2但小于0.2的版本
 pod ‘AFNetworking’, ‘~>0.1’ //使用大于等于0.1但小于1.0的版本
 pod ‘AFNetworking’, ‘~>0’ //高于0的版本，写这个限制与什么都不写是同样效果，皆表示使用最新版本



作者：彭磊PL
链接：https://www.jianshu.com/p/118bbfba5c23
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。