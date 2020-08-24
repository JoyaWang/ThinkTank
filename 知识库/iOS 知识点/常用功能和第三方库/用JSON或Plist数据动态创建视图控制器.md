# 用JSON或Plist数据动态创建视图控制器



```json
# main.json


[
  {
    "title" : "首页",
    "imageName" : "tab_home",
    "clsName" : "JLHomeViewController"
  },
  {
    "title" : "分类",
    "imageName" : "tab_fenlei",
    "clsName" : "JLClassificationViewController"
  },
  {
    "title" : "客服",
    "imageName" : "tab_kefu",
    "clsName" : "ViewController"
  },
  {
    "title" : "买家秀",
    "imageName" : "tab_maijiaxiu",
    "clsName" : "JLBuyerViewController"
  },
  {
    "title" : "我",
    "imageName" : "tab_wode",
    "clsName" : "JLProfileViewController"
  }
]

```



## Objc

```objc
//
//  JLMainViewController.m
//  JewelryMall
//
//  Created by Joya Wang on 2020/4/9.
//  Copyright © 2020 Joya Wang. All rights reserved.
//

#import "JLMainViewController.h"
#import "CZAdditions.h"
#import "JLNavigationController.h"

@interface JLMainViewController ()

@end

@implementation JLMainViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view.
    [self setupChildControllers];
}


- (void)setupChildControllers {
    // 从本地 bundle 获取 main.json 的路径
    NSURL *url = [NSBundle.mainBundle URLForResource:@"main.json" withExtension:nil];
    
    // 加载 main.json 中的子控制器数据
    NSData *data = [NSData dataWithContentsOfURL:url];
    
    // 反序列化获取到数据数组
    NSArray *arr = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];
    
    NSMutableArray *mArr = [[NSMutableArray alloc] initWithCapacity:5];
    
    for (NSDictionary *dict in arr) {
        [mArr addObject:[self controllerWith:dict]];
    }
    self.viewControllers = mArr;
}

/// 用字典创建视图控制器
/// @param dict 包含视图控制器信息的字典
- (UIViewController *) controllerWith:(NSDictionary *)dict {
    
//    NSString *clsName = [self.nameSpace stringByAppendingFormat:@".%@",dict[@"clsName"]];
    
    // 从数据字典中加载 控制器的信息
    NSString *clsName = dict[@"clsName"];
    NSString *imageName = dict[@"imageName"];
    NSString *title = dict[@"title"];
    
    
    // 创建视图控制器
    UIViewController *vc = [[NSClassFromString(clsName) alloc] init];
    
    // 如果 vc 为空，则返回一个常见 VC
    vc == nil ? vc = [UIViewController new] : nil;
    
    // 设置视图控制器的 背景颜色
//    vc.view.backgroundColor = UIColor.cz_randomColor;
    
    // 设置视图控制器 在 tabBar 的标题
    vc.tabBarItem.title = title;
    
    // 设置 tabbar 字体颜色
    [vc.tabBarItem setTitleTextAttributes:
     @{
         // 设置 字体 和 大小
         NSFontAttributeName: [UIFont fontWithName:@"PingFang SC" size: 11],
         // 设置 字体颜色
         NSForegroundColorAttributeName : [UIColor cz_colorWithRed:204 green:127 blue:90]
     } forState:UIControlStateNormal];
    
    // 设置 此控制器 在 tabBar 的显示图片
    UIImage *normalImage = [[UIImage imageNamed:[imageName stringByAppendingString:@"_nor"]] imageWithRenderingMode:UIImageRenderingModeAlwaysOriginal];
    UIImage *selectedImage = [[UIImage imageNamed:[imageName stringByAppendingString:@"_sel"]] imageWithRenderingMode:UIImageRenderingModeAlwaysOriginal];
    
    // 设置 未选中 的图片
    vc.tabBarItem.image = normalImage;
    // 设置 选中 的图片
    vc.tabBarItem.selectedImage = selectedImage;
    // 给每个控制器外面包一个导航控制器
    JLNavigationController *naVc = [[JLNavigationController alloc] initWithRootViewController:vc];
    
    return naVc;
}

@end


```



## Swift

```swift

    // 设置 子控制器
    private func setupChildControllers() {
        
        // 判断沙盒是不是有从网络获取的最新的视图配置信息 JSON 文件
        let docPath = NSSearchPathForDirectoriesInDomains(.documentDirectory, .userDomainMask, true)[0]
        let docUrl = URL(fileURLWithPath: docPath)
        let fileURL = docUrl.appendingPathComponent("main.json")
        var data = try? Data(contentsOf: fileURL)
        
        // 如果沙盒中没有，则加载本地的配置文件
        if data == nil {
            let url = Bundle.main.url(forResource: "main.json", withExtension: nil)
            data = try? Data(contentsOf: url!)
        }
        
        // 1. 路径URL/ 2. 加载 data/ 3. JSON 反序列化
        guard let arr = try? JSONSerialization.jsonObject(with: data!, options: []) as? Array<[String:Any]> else {
                return
        }
        
        // 将所有控制器遍历添加为主控制器的子控制器
        // 不能用 ViewControllers 直接添加，是 nil，不会调用 append 方法
        var mArr = [UIViewController]()
        for dict in arr {
            mArr.append(controller(dict: dict))
        }
        viewControllers = mArr
    }
    
    /// 使用字典创建一个子控制器
    /// - Parameter dict: 保存控制器信息的字典[clsName, title, imgName, visitorInfo]
    private func controller (dict:Dictionary<String, Any>) -> UIViewController {
        // 1. 取得字典内容
        guard let clsName = dict["clsName"] as? String,
            let title = dict["title"] as? String?,
            let imageName = dict["imageName"] as? String,
            let vcClass = NSClassFromString(self.nameSpace + "." + clsName) as? JLBaseViewController.Type,
            let visitorDict = dict["visitorInfo"] as? [String:String]
            else {
            return UIViewController()
        }
//        print(self.nameSpace + "." + clsName)
        
        // 2. 创建视图控制器
        let vc = vcClass.init()
        
        // 设置控制器的访客信息字典
        vc.visitorInfoDict = visitorDict
        
        // 3. 设置此控制器在 tabBar 的图片
        vc.tabBarItem.image = UIImage.init(named: "tabbar_" + imageName)?.withRenderingMode(.alwaysOriginal)
        vc.tabBarItem.selectedImage = UIImage.init(named: "tabbar_" + imageName + "_selected")?.withRenderingMode(.alwaysOriginal)
        
        // 4.设置此控制器在 tabbar 的标题和字体颜色
        vc.title = title
        vc.tabBarItem.setTitleTextAttributes([NSAttributedString.Key.foregroundColor:UIColor.orange], for: .highlighted) // 设置字体颜色
//        vc.tabBarItem.setTitleTextAttributes([NSAttributedString.Key.font:UIFont.systemFont(ofSize: 20)], for: .normal) // 设置字体大小，默认12
        // 实例化导航控制器的时候，会调用 push 方法将 rootVC 压栈
        let nav = JLNavigationController(rootViewController: vc)// 包裹在导航控制器中返回
        return nav
    }
}
```

