# ScrollView 中 子控件的布局

- 设置 有导航控制器时, scrollView 不自动调整自己的原点

  ```objc
self.edgesForExtendedLayout = UIRectEdgeNone;
  
  self.automaticallyAdjustsScrollViewInsets = YES;
  ```
  
  

- ### 使用 containerView

  - 如果只有一个子视图, 且scrollView高度由子视图确定的话.

    ```objc
    // MARK: - 布局子控件
    - (void)viewDidLayoutSubviews {
        [super viewDidLayoutSubviews];
        // 布局 scrollView
        [self.scrollView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.edges.equalTo(self.view);
        }];
        
        // 布局 容器视图
        [self.containerView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.edges.equalTo(self.scrollView);
            make.width.equalTo(self.scrollView);
            // 已保证scrollView 的contentSize 随着 containerView 的size 变化, 但是 container的高度未确定
        }];
        
        // 布局 imgView
        [self.imgView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.leading.top.trailing.mas_equalTo(0);
        }];
        
        // 最后, 通过设置 container 的底部与最后一个子控件图片框的底部相同, 从而设置了 container 的高度与图片相同, 从而使得 scrollView 的高度与 图片相同
        [self.containerView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.bottom.equalTo(self.imgView.mas_bottom);
        }];
    }
    ```

  - 如果有多个子控件

    ```objc
    - (void)viewDidLayoutSubviews {
        [super viewDidLayoutSubviews];
        // 布局子控件
        // 设置scrollView约束
        [self.scrollView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.edges.equalTo(self.view);
        }];
        // 设置参照视图的约束
        [self.contentView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.edges.equalTo(self.scrollView);
            make.width.equalTo(self.scrollView);
    //        make.height.greaterThanOrEqualTo(@0.0f);
        }];
        // 第一个测试view的约束
        [self.oneView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.top.equalTo(self.contentView).offset(30);
            make.left.equalTo(self.contentView);
            make.width.mas_equalTo(200);
            make.height.mas_equalTo(300);
        }];
        // 第二个测试view的约束
        [self.twoView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.top.equalTo(self.oneView.mas_bottom).offset(50);
            make.right.equalTo(self.contentView);
            make.width.mas_equalTo(400);
            make.height.mas_equalTo(500);
        }];
        // 第三个测试view的约束
        [self.threeView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.top.equalTo(self.twoView.mas_bottom).offset(70);
            make.left.right.equalTo(self.contentView);
            make.height.mas_equalTo(300);
        }];
        // 最后设置最后一个view的与参照容器view的约束
        [self.contentView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.bottom.equalTo(self.threeView.mas_bottom).offset(-10);
        }];
    }
    ```

    

- ### 不使用 containerView

  - 如果只有一个子视图, 且scrollView高度由子视图确定的话.

    > - Edges都为0, 只是说明它的大小会随着父控件变化, 并不意味着它的 contentSize 就确定了, 只有父控件的大小确定了才行
    > - 将 scrollView 的edges 都equal to 它的父控件, 或者要显示的大小.
    > - 布局 scrollView 的子控件, 如果是动态高度的话, 只先布局它除去高度外的约束
    > - 最后, 设置 scrollView 的 bottom 与最后一个子控件的bottom 相等, 相当于确定了 scrollView 的高度

    ```objc
    // MARK: - 布局子控件
    - (void)viewDidLayoutSubviews {
        [super viewDidLayoutSubviews];
        // 布局 scrollView
        [self.scrollView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.edges.equalTo(self.view);
        }];
        
        // 布局 imgView
        [self.imgView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.edges.equalTo(self.scrollView);
            make.width.equalTo(self.scrollView);
            // 已保证scrollView 的contentSize 随着 imgView 的size 变化, 但是 scrollView contentSize的高度仍未确定
        }];
        
        // 最后, 通过设置 scrollView 的底部与最后一个子控件imgView的底部相同,从而使得 scrollView 的高度与 图片相同
        [self.scrollView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.bottom.equalTo(self.imgView.mas_bottom);
        }];
    }
    ```

    

