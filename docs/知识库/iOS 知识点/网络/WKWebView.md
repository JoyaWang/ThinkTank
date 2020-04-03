# WKWebView

> webView/WKWebView【详见Practices中的webView & HTML & JavaScript】
>
> [WKWebView的使用详解](https://blog.csdn.net/xj_love/article/details/52062874?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task)



> 实例应用
>
> - Practices中的webView & HTML & JavaScript
>
> - 彩票设置界面
>
>   跳转到网页的指定位置
>
> - JL微博_JLOAuthViewController
>
>   自动填充用户名密码功能

- ### webView 的用途

  > 可加载本地doc、pdf、mp4、html等文件

- ### 使用

  - 自动检测网页中的电话、邮件地址、链接

    ```objc
    // 在创建webView时，用configuration设置【WKWebView】
    WKWebViewConfiguration *config = [[WKWebViewConfiguration alloc] init];
    config.dataDetectorTypes = WKDataDetectorTypeAll;
    WKWebView *wv = [[WKWebView alloc] initWithFrame:UIScreen.mainScreen.bounds configuration:config];
    
    // 【webView，已废弃】
    dataDetectorTypes = UIDataDetectorTypeAll 
    ```

- ### iOS APP 与 HTML 交互

  - iOS 的控件执行 JavaScript 代码控制 Html5 页面的变化

    > - `WKWebView` 在用
    >
    >   > 先设置WKWebView的navigationDelegate
    >   >
    >   > 在代理方法didFinishNavigation中调用 [webView evaluateJavaScript:code completionHandler:**nil**];
    >
    > - `webView` 已废弃
    >
    >   > 先设置webView的代理，在代理方法webViewDidFinishLoad里面调用下面方法
    >   >
    >   > [webView stringByEvaluatingJavaScriptFromString:]

  - webView 加载的 html5 页面上的控件执行 iOS 的方法

    > - `WKWebView` 在用
    >
    >   > - 将JavaScript中要调用的OC方法名先注册到wkWebView.configuration.userContentController中【只写一个方法名即可】
    >   >
    >   >   [wv.configuration.userContentController addScriptMessageHandler:**self** name:@"showAlert"];
    >   >
    >   > - 遵守WKScriptMessageHandler协议，在协议方法userContentController didReceiveScriptMessage中拦截已注册的方法名并进行本地处理【在这里实现JS要调用的方法】
    >   >
    >   > - 在此页面销毁时，移除注册的方法，否则会造成内存泄漏[wv.configuration.userContentController removeScriptMessageHandlerForName:@"showAlert"]
    >   >
    >   > - 在HTML5的JavaScript中使用window.webkit.messageHandlers.showAlert.postMessage("我是来自HTML网页里JavaScript中的消息");调用注册的方法
    >   >
    >   >   showAlert为注册的方法名
    >   >
    >   >   postMessage中为传递给该方法的参数
    >
    > - `webView` 已废弃
    >
    >   > - 先在html中创建一个超链接
    >   >
    >   >   ```html
    >   >   <a href="source:///showMessage:/helloword">调用OC的方法</a>
    >   >   ```
    >   >
    >   >   > [source:///](source:///) 自定义协议
    >   >   >
    >   >   > showMessage:方法名、方法参数
    >   >   >
    >   >   > helloword 参数
    >   >
    >   > - 在webView的代理方法中
    >   >
    >   > - 从request获取协议信息、方法名、参数
    >   >
    >   >   > request.URL.scheme协议信息
    >   >   >
    >   >   > request.URL.pathComponents[1] 方法名
    >   >   >
    >   >   > request.URL.pathComponents[2] 参数
    >   >
    >   > - 通过方法名创建SEL
    >   >
    >   > - 判断respondsToSelector后，使用performSelector执行这个SEL对象

- ### delegate 方法

  - WKNavigationDelegate

    > - 页面开始加载时调用
    >
    >   > didStartProvisionalNavigation
    >
    > - 当内容开始返回时调用
    >
    >   > didCommitNavigation
    >
    > - 页面加载完成之后调用
    >
    >   > didFinishNavigation
    >
    > - 页面加载失败时调用
    >
    >   > didFailProvisionalNavigation
    >
    > - 接收到服务器跳转请求之后调用
    >
    >   > didReceiveServerRedirectForProvisionalNavigation
    >
    > - 在收到响应后，决定是否跳转
    >
    >   > decidePolicyForNavigationResponse
    >
    > - 在发送请求之前，决定是否跳转
    >
    >   > decidePolicyForNavigationAction

  - WKUIDelegate