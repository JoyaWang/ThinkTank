# AFNetworking 使用

- 获取请求信息和响应信息

  ```objc
  [manager GET:requestUrl parameters:request.requestParams progress:^(NSProgress * _Nonnull downloadProgress) {
          } success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {
              [request requestCompletionCallback:task responseObject:responseObject];
              
              self.infoDict[@"请求URL"] = task.originalRequest.URL;
              self.infoDict[@"请求出错信息"] = error;
              self.infoDict[@"响应体"] = responseObject;
              self.infoDict[@"请求方式"] = task.originalRequest.HTTPMethod;
              NSHTTPURLResponse *rp = (NSHTTPURLResponse *)task.response;
              self.infoDict[@"响应状态码"] = @([rp statusCode]);
              self.infoDict[@"请求头信息"] = task.originalRequest.allHTTPHeaderFields;
              self.infoDict[@"请求正文信息"] = task.originalRequest.allHTTPHeaderFields;
              
          } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
              [request requestFailedCallback:task error:error];
              
              
          }];
  ```

  

- **AFURLSessionManager**

- **AFHTTPSessionManager**

  - GET登录

  - POST登录

  - 下载

    > 返回存储文件的路径URL
    >
    > 获取进度：对progress的fractionCompleted进行KVO
    >
    > 断点续传

  - 上传

- 当从网络获取数据时，显示菊花

  ```objc
    [[AFNetworkActivityIndicatorManager sharedManager] setEnabled:YES];
  ```

- 设置缓存文件夹名称和缓存大小

  ```objc
  // 设置缓存
      /*
       内存缓存: 5M
       磁盘缓存: 10M
       缓存文件夹名称: joyaImages
       */
      NSURLCache *cache = [[NSURLCache alloc] initWithMemoryCapacity:1024*1024*5 diskCapacity:1024*1024*10 diskPath:@"joyaImages"];
      [NSURLCache setSharedURLCache:cache];
  ```


NSURLSessionDataTask

responseSerializer

AFJSONResponseSerializer 默认初始化器是JSON

[AFHTTPResponseSerializer serializer] 而百度返回的是HTML，所以需要设置为AFHTTPResponseSerializer

responseObject

requestSerializer

AFJSONRequestSerializer serializer

设置请求头



```objc
//
//  ViewController.m
//  Day06 - AFNetworking演示
//
//  Created by Joya Wang on 2020/1/28.
//  Copyright © 2020 Joya Wang. All rights reserved.
//

#import "ViewController.h"
#import "AFHTTPSessionManager.h"
#import "JLVideo.h"

@interface ViewController () <NSXMLParserDelegate>
@property (nonatomic, strong) JLVideo *video;
@property (nonatomic, copy) NSMutableString *mString;
@property (nonatomic, strong) NSMutableArray *videos;

@end

@implementation ViewController

- (NSMutableString *)mString {
    if (!_mString) {
        _mString = [NSMutableString string];
    }
    return _mString;
}
- (NSMutableArray *)videos {
    if (!_videos){
        _videos = [NSMutableArray arrayWithCapacity:10];
    }
    return _videos;
}

- (void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
    [self getXML];
}

// 发送GET请求，获取JSON文件响应
- (void) get1 {
    [[AFHTTPSessionManager manager] GET:@"http://127.0.0.1/Vocabularies.json" parameters:nil headers:nil progress:^(NSProgress * _Nonnull downloadProgress) {
        
    } success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {
        NSLog(@"%@", responseObject);
    } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
        if (error) {
            NSLog(@"发送GET请求出错: %@", error);
        }
    }];
}

// 发送GET请求，获取JSON文件响应(将用户名和密码以URL参数形式传入登录)
- (void) get2 {
    [[AFHTTPSessionManager manager] GET:@"http://127.0.0.1/php/login.php" parameters:@{@"username":@"admin", @"password" : @"123"} headers:nil progress:nil success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {
        NSLog(@"%@", responseObject);
    } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
        if (error) {
            NSLog(@"发送GET请求错误: %@", error);
        }
    }];
}

// 发送POST请求，获取JSON文件响应(将用户名和密码以参数形式传入请求体登录)
- (void) post {
    [[AFHTTPSessionManager manager] POST:@"http://127.0.0.1/php/login.php" parameters:@{@"username":@"admin", @"password":@"123456"} headers:nil progress:nil success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {
        NSLog(@"%@", responseObject);
    } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
        if (error) {
            NSLog(@"发送POST请求失败: %@", error);
        }
    }];
}

// 下载
- (void) download {
    NSURL *url = [NSURL URLWithString:@"http://127.0.0.1/v.mp4"];
    NSURLRequest *request = [NSURLRequest requestWithURL:url];
    
    
    [[[AFHTTPSessionManager manager] downloadTaskWithRequest:request progress:^(NSProgress * _Nonnull downloadProgress) {
                
        NSLog(@"%@", downloadProgress);
        
        // 使用KVO实时观察downloadProgress的属性的变化
        /*
         参数1: 被观察的属性属于的对象
         参数2: 要被观察的属性
         参数3 context: 要传给观察的方法的参数
         */
        [downloadProgress addObserver:self forKeyPath:@"fractionCompleted" options:NSKeyValueObservingOptionNew context:nil];
        
    } destination:^NSURL * _Nonnull(NSURL * _Nonnull targetPath, NSURLResponse * _Nonnull response) {
        
        NSLog(@"文件临时路径: %@", targetPath);
        
        // 创建要保存文件的地址
        NSString *filePath = [[NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES) lastObject] stringByAppendingPathComponent:response.suggestedFilename];
        
        // 创建FileURL并返回
        NSURL *url = [[NSURL alloc] initFileURLWithPath:filePath];
        
        return url;
        
    } completionHandler:^(NSURLResponse * _Nonnull response, NSURL * _Nullable filePath, NSError * _Nullable error) {
        
        if (filePath) {
            NSLog(@"下载成功: %@", filePath);
        }
        
        if(error) {
            NSLog(@"下载文件出错: %@", error);
        }
    }] resume];
}

// 观察某对象的属性变化调用的方法
/*
 参数keyPath: 观察的对象被观察的属性
 参数object: 观察的对象
 参数change: 观察的属性发生的变化
 参数context: 对应上面的context，传过来的参数
 */
- (void) observeValueForKeyPath:(NSString *)keyPath ofObject:(id)object change:(NSDictionary<NSKeyValueChangeKey,id> *)change context:(void *)context {
    if ([object isKindOfClass:[NSProgress class]]) {
        NSProgress *progress = object;
        NSLog(@"%@",progress.localizedDescription);
        NSLog(@"%@", progress.localizedAdditionalDescription);
        NSLog(@"completedUnitCount : %lld", progress.completedUnitCount);
        NSLog(@"totalUnitCount: %lld", progress.totalUnitCount);
        NSLog(@"fractionCompleted: %f", progress.fractionCompleted);
    }
}

// 发送HTTP中的GET请求，获取HTML格式的字符串数据响应【须修改默认的响应初始化器】
-(void) getBaidDu {
    // 创建Manager
    AFHTTPSessionManager *manager = [AFHTTPSessionManager manager];
    
    // 因为默认初始化器是JSON的(AFJSONResponseSerializer)，而百度返回的是HTML，所以需要设置为AFHTTPResponseSerializer
    manager.responseSerializer = [AFHTTPResponseSerializer serializer];
    
    // 发送HTTP请求
    [manager GET:@"https://www.baidu.com" parameters:nil headers:nil progress:nil success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {
        NSString *str = [[NSString alloc] initWithData:responseObject encoding:NSUTF8StringEncoding];
        NSLog(@"获取到网页: %@", str);
    } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
        if (error) {
            NSLog(@"获取网页出错: %@", error);
        }
    }];
}


-(void) getXML {
    
    AFHTTPSessionManager *manager = [AFHTTPSessionManager manager];
    
    manager.responseSerializer = [AFXMLParserResponseSerializer serializer];
    
    [manager GET:@"http://127.0.0.1/videos.xml" parameters:nil headers:nil progress:nil success:^(NSURLSessionDataTask * _Nonnull task, id  _Nullable responseObject) {
        NSLog(@"%@", responseObject);
        NSXMLParser *parser = (NSXMLParser *)responseObject;
        parser.delegate = self;
        [parser parse];
    } failure:^(NSURLSessionDataTask * _Nullable task, NSError * _Nonnull error) {
        NSLog(@"%@", error);
    }];
    
}

// 开始解析XML文档
- (void)parserDidStartDocument:(NSXMLParser *)parser {
    NSLog(@"开始解析XML");
}
// 开始解析节点
- (void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName attributes:(NSDictionary<NSString *,NSString *> *)attributeDict {
    
    NSLog(@"Start Element: %@", elementName);
    
    if ([elementName isEqualToString:@"video"]) {
        self.video = [JLVideo new];
        self.video.videoId = @([attributeDict[@"videoId"] intValue]);
    }

}
// 开始解析节点之间的内容
- (void)parser:(NSXMLParser *)parser foundCharacters:(NSString *)string {
    NSLog(@"内容: %@", string);
    [self.mString appendString:string];
}

// 解析节点完毕
- (void)parser:(NSXMLParser *)parser didEndElement:(NSString *)elementName namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName {
    NSLog(@"End Element: %@", elementName);
    
    if ([elementName isEqualToString:@"video"]) {
        [self.videos addObject:self.video];
    } else if (![elementName isEqualToString:@"videos"]){
        [self.video setValuesForKeysWithDictionary:@{elementName : self.mString}];
        self.mString = nil;
    }
}
// 结束解析XML文档
- (void)parserDidEndDocument:(NSXMLParser *)parser {
    NSLog(@"XML文件解析完毕");
    NSLog(@"%@", self.videos);
}

@end

```

