# NSCache 缓存

```objc

- (NSCache *)cache {
    if(!_cache) {
        _cache = [[NSCache alloc] init];
        _cache.countLimit = 5;
        _cache.delegate = self;
    }
    return _cache;
}

- (void)cache:(NSCache *)cache willEvictObject:(id)obj {
    NSLog(@"从缓存中移除%@", obj);
}

- (void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
    // 往缓存中存储数据
    for (int i = 1; i <= 10; i++) {
        [self.cache setObject:[NSString stringWithFormat:@"Hello%d",i] forKey:[NSString stringWithFormat:@"h%d",i]];
        NSLog(@"添加%@",[NSString stringWithFormat:@"Hello%d",i]);
    }
    // 输出缓存中的数据
    for (int i = 1; i <= 10; i++) {
        NSLog(@"%@", [self.cache objectForKey:[NSString stringWithFormat:@"h%d",i]]);
    }
}

- (void)didReceiveMemoryWarning {
    // 输出缓存中的数据
    for (int i = 1; i <= 10; i++) {
        NSLog(@"%@", [self.cache objectForKey:[NSString stringWithFormat:@"h%d",i]]);
    }
}


```

