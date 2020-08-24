# APP启动加载自定义控制器

> iOS13之前没有SceneDelegate，只从AppDelegate那开始加载自定义控制器就行了。
>
> iOS13之后，在AppDelegate和SceneDelegate都要加载。
>
> 这样，iOS13之前的用户从AppDelegate走，iOS13之后的用户从SceneDelegate走





## Objc



```objc
// AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after application launch.
    
    // 创建 window
    UIWindow *window = [[UIWindow alloc] initWithFrame:kScreenBounds];
    
    // 设置 window
    self.window = window;
    
    // 创建登录控制器
    JLLoginViewController *loginVC = [JLLoginViewController viewControllerFromXib];
    
    // 创建主控制器
    JLMainViewController *mainVC = [[JLMainViewController alloc] init];

    // 将主控制器设置为 window 的根控制器
    self.window.rootViewController = loginVC;
    
    // 使 window 可见
    [self.window makeKeyAndVisible];
    
    
    return YES;
}

```



```objc
// SceneDelegate

- (void)scene:(UIScene *)scene willConnectToSession:(UISceneSession *)session options:(UISceneConnectionOptions *)connectionOptions  API_AVAILABLE(ios(13.0)){
    
    // 创建 WindowScene
    UIWindowScene *windowScene = (UIWindowScene *)scene;
    
    // 创建 window
    UIWindow *window = [[UIWindow alloc] initWithWindowScene:windowScene];
    
    // 设置 window
    self.window = window;
    
    // 创建登录控制器
    JLLoginViewController *loginVC = [JLLoginViewController viewControllerFromXib];
    
    // 创建主控制器
    JLMainViewController *mainVC = [[JLMainViewController alloc] init];

    // 将主控制器设置为 window 的根控制器
    self.window.rootViewController = mainVC;
    
    // 使 window 可见
    [self.window makeKeyAndVisible];
    
    // 解决 SVProgressHUD 的bug
    AppDelegate *appDelegate = (AppDelegate *) UIApplication.sharedApplication.delegate;
    appDelegate.window = self.window;
    
}

```



## Swift



```swift
// AppDelegate
var window: UIWindow?

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        // Override point for customization after application launch.
        
        
        let vc = JLSettingsController()
        vc.plistName = "SettingsList"
        
        let w = UIWindow(frame: UIScreen.main.bounds)
        window = w
        window?.rootViewController = vc
        window?.makeKeyAndVisible()
        
        
        return true
    }
```



```swift
// SceneDelegate
func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
        
        guard let windowScene = (scene as? UIWindowScene) else { return }
        
        let window = UIWindow(windowScene: windowScene)
        self.window = window
        
        let mainVC = JLMainViewController()
        mainVC.view.backgroundColor = UIColor.red
        
        self.window?.rootViewController = mainVC
        
        self.window?.makeKeyAndVisible()
    }

```

