# XLForm

将要显示表单的视图控制器设置为XLForm的子类

- 创建表

  设置表标题

- 创建组

  设置组标题

- 创建行

  设置行标题和行值

  取行标题和输入的值

  - 行为按钮

    ```
    row = [XLFormRowDescriptor formRowDescriptorWithTag:@"submitButton" rowType:XLFormRowDescriptorTypeButton title:@"提交"];
        row.action.formSelector = @selector(submitTapped);
        [section addFormRow:row];
    ```

    

- 取表单中所有行的值

  - formVC.formValues

- 设置行高

- 设置表单背景颜色

  ```onjc
  - (void)viewDidLoad {
      [super viewDidLoad];
      self.tableView.backgroundColor = UIColor.whiteColor;
  }
  ```

- 设置组头自定义视图

- 设置组头高度

- 设置组尾自定义视图

- 设置组尾高度

- 自定义Row的cell

  - 步骤

    > - 自定义cell要继承自XLFormBaseCell类
    >
    > - 重写三个方法
    >
    >   - +(**void**)load 
    >
    >     > 【非必须】可以在这里，在主表单中注册此自定义cell以及对应的ID
    >
    >   - \- (**void**)configure
    >
    >     > 【必须】在这里进行UI搭建和配置
    >
    >   - \- (**void**)update
    >
    >     > 【必须】外面给控件赋值以后就会调用这个？可以在这里进行赋值后的操作
    >
    > - 在创建row时
    >
    >   > - 必须使用自定义cell的ID(type)
    >   >
    >   >   > row = [XLFormRowDescriptor formRowDescriptorWithTag:@"phone" rowType:`kInputInfoCellType`];
    >   >
    >   > - 必须设置row的cellClass为自定义cell，否则会出现错误
    >   >
    >   >   > row.cellClass = [`ECInputInfoCell class`]; 

  - 从自定义的cell中将 **控件的值** 传出去

    > 在需要将值传出去的地方，将值存到**self**.rowDescriptor.value中，value应该是id类型的，所以可以直接赋值传一个值，也可以以数组或者字典的形式传出去多个值。

  - 从自定义的cell中将 **点击事件** 传出去

    > 使用 代理 的方式
    >
    > - 为cell创建代理协议，在其中声明要传出去的事件方法
    > - 为cell设置 weak  的 delegate属性
    > - 在需要传递点击事件的时候，调用 delegate 中声明的相应方法
    > - 在创建row的时候，通过 `[row.cellConfig setObject:self forKey:@"delegate"];` 将formVC设置为自定义cell的代理
    > - 在 formVC 中实现自定义 cell 中的代理方法
    > - 这样自定义cell中的事件就能传递出来了

  - 自定义cell代码片段

    ```
    // 自定义cell.h文件
    @class ECInputInfoCell;
    @protocol ECInputInfoCellDelegate <NSObject>
    
    /// 用户点击按钮(验证码按钮回调)
    /// @param cell cell
    /// @param btn 按钮
    - (void)ECInputInfoCell:(ECInputInfoCell *)cell verifyCodeButtonTapped:(UIButton *)btn;
    
    /// 输入框中文字变化时调用
    /// @param cell cell
    /// @param textField 输入框
    - (void)ECInputInfoCell:(ECInputInfoCell *)cell textFieldEditingChanged:(UITextField *)textField;
    
    /// 输入框输入完毕，释放了第一响应者以后调用
    /// @param cell cell
    /// @param textField 输入框
    - (void)ECInputInfoCell:(ECInputInfoCell *)cell textFieldDidEndEditing:(UITextField *)textField;
    
    @end
    -------------------------------------------------------------------------------------
    // 自定义cell.m文件
    @interface ECInputInfoCell ()<UITextFieldDelegate>
    
    @property (nonatomic, strong) UILabel *leftLabel; // 左边的文本框
    @property (nonatomic, strong) UITextField *rightTextField; // 右边的输入框
    @property (nonatomic, strong) UIButton *btn; // 按钮
    @property (nonatomic, strong) UIView *separatorView; // 分割线
    @property (nonatomic, weak)id <ECInputInfoCellDelegate> delegate; // 代理
    
    @end
    
    @implementation ECInputInfoCell
    
    
    +(void)load {
        // 在主表单中注册此自定义cell以及对应的ID
        [XLFormViewController.cellClassesForRowDescriptorTypes setObject:[ECInputInfoCell class] forKey:kInputInfoCellType];
    }
    
    // 这个方法是用来设置属性的 必须重写  类似于初始化的属性不变的属性进行预先配置
    - (void)configure {
        [super configure];
        self.selectionStyle = UITableViewCellSelectionStyleNone;// 取消选中时cell为灰色
        [self setupUI]; // 搭建UI
    }
    
    /// 搭建界面
    - (void)setupUI {
        // 添加文本框
        [self.contentView addSubview:self.leftLabel];
        // 添加按钮
        [self.contentView addSubview:self.btn];
        // 添加输入框
        [self.contentView addSubview:self.rightTextField];
        self.rightTextField.delegate = self;
        // 添加分割线
        [self.contentView addSubview:self.separatorView];
        // 设置约束
        [self setupConstraints];
    }
    
    /// 设置约束
    - (void) setupConstraints {
        [self.leftLabel mas_makeConstraints:^(MASConstraintMaker *make) {
            make.leading.mas_equalTo(30);
            make.bottom.mas_equalTo(-4);
            make.width.mas_equalTo(80);
        }];
        
        [self.rightTextField mas_makeConstraints:^(MASConstraintMaker *make) {
            make.leading.equalTo(self.leftLabel.mas_trailing).offset(12.5);
            make.trailing.equalTo(self.btn.mas_leading);
            make.bottom.mas_equalTo(-4);
        }];
        
        [self.btn mas_makeConstraints:^(MASConstraintMaker *make) {
            make.size.mas_equalTo(CGSizeMake(76, 23));
            make.trailing.mas_equalTo(-30);
            make.bottom.mas_equalTo(-4);
        }];
        
        [self.separatorView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.leading.mas_equalTo(30);
            make.height.mas_equalTo(0.5);
            make.trailing.mas_equalTo(-30);
            make.bottom.mas_equalTo(0.5);
        }];
    }
    
    
    // 这个方法是用来进行更新的，外面给唯一的字段Value设定值就好了 通过self.rowDescriptor.value的值变化来进行更新
    - (void)update
    {
        [super update];
        // 接收值并赋给控件
        self.leftLabel.text = self.rowDescriptor.title;
        // leftLabel 接到值以后，可以用来判断
        if ([self.leftLabel.text isEqualToString:@"短信验证码"]) {
            [self.btn setHidden:NO];
        }
        if ([self.leftLabel.text isEqualToString:@"手机号码"]) {
            self.rightTextField.keyboardType = UIKeyboardTypeNumberPad;
        }
        if ([self.leftLabel.text isEqualToString:@"登录密码"]) {
            self.rightTextField.secureTextEntry = YES;
        }
    }
    
    /// 用户点击验证码按钮
    /// @param sender 验证码按钮
    - (void)btnTapped:(UIButton *)sender {
        [self.delegate ECInputInfoCell:self verifyCodeButtonTapped:self.btn];
    }
    /// 文本框中的文字变化时调用
    - (void)textFieldValueDidChanged:(UITextField *)textField {
        // 在这里把自定义cell获取到用户输入的信息传递出去【去除空格和回车】
        self.rowDescriptor.value = [self.rightTextField.text stringByTrimmingCharactersInSet:[NSCharacterSet whitespaceAndNewlineCharacterSet]];
        [self.delegate ECInputInfoCell:self textFieldEditingChanged:textField];
    }
    /// 文本框已经结束编辑(已经释放第一响应者)
    - (void)textFieldDidEndEditing:(UITextField *)textField {
        [self.delegate ECInputInfoCell:self textFieldDidEndEditing:textField];
    }
    
    
    - (UILabel *)leftLabel {
        if (!_leftLabel) {
            _leftLabel = [UILabel new];
            _leftLabel.font = FONT15;
            _leftLabel.textColor = OWNER_HOMEVIEW_CELL_TITLE;
        }
        return _leftLabel;
    }
    
    - (UITextField *)rightTextField {
        if (!_rightTextField) {
            _rightTextField = [UITextField new];
            _rightTextField.font = FONT15;
            [_rightTextField addTarget:self action:@selector(textFieldValueDidChanged:) forControlEvents:UIControlEventEditingChanged];
        }
        return _rightTextField;
    }
    
    - (UIView *)separatorView {
        if (!_separatorView) {
            _separatorView = [UIView new];
            _separatorView.backgroundColor = QUOTATION_SPEC_GRAY;
        }
        return _separatorView;
    }
    
    - (UIButton *)btn {
        if (!_btn) {
            _btn = [UIButton new];
            [_btn setTitle:@"验证码" forState:UIControlStateNormal];
            _btn.backgroundColor = UIColorFromRGB(0x326EF0);
            _btn.layer.cornerRadius = 3.0;
            _btn.titleLabel.font = FONT12;
            [_btn setHidden:YES];
            [_btn addTarget:self action:@selector(btnTapped:) forControlEvents:UIControlEventTouchUpInside];
        }
        return _btn;
    }
    
    @end
    
    ```

  - formVC

    ```
    //
    //  ECModifyPhoneNumViewController.m
    //  cloudExchange
    //
    //  Created by Joya Wang on 2020/6/2.
    //  Copyright © 2020 高武. All rights reserved.
    //
    
    #import "ECModifyPhoneNumViewController.h"
    #import "ECInputInfoCell.h"
    #import "ECBaseRequest.h"
    #import "ECBaseResponse.h"
    #import "NSString+PJR.h"
    
    @interface ECModifyPhoneNumViewController ()<ECInputInfoCellDelegate>
    {
        ECBaseRequest *_verifyCodeRequest;
        ECBaseRequest *_modifyPhoneNumRequest;
    }
    @end
    
    @implementation ECModifyPhoneNumViewController
    
    - (instancetype)initWithNibName:(NSString *)nibNameOrNil bundle:(NSBundle *)nibBundleOrNil {
        self = [super initWithNibName:nibNameOrNil bundle:nibBundleOrNil];
        if (self){
            [self initializeForm];
        }
        return self;
    }
    
    - (id)initWithCoder:(NSCoder *)aDecoder {
        self = [super initWithCoder:aDecoder];
        if (self){
            [self initializeForm];
        }
        return self;
    }
    
    - (void)initializeForm {
      // Implementation details covered in the next section.
        XLFormDescriptor * form; // 列表
        XLFormSectionDescriptor * section; // 分组
        XLFormRowDescriptor * row; // 列
        
        form = [XLFormDescriptor formDescriptorWithTitle:@""]; // 设置标题
    
        // 第一组
        section = [XLFormSectionDescriptor formSection];
    //    section.title = @"更改手机号";
        [form addFormSection:section];
    
        // 手机号码
        row = [XLFormRowDescriptor formRowDescriptorWithTag:@"phone" rowType:kInputInfoCellType];
        row.cellClass = [ECInputInfoCell class];
        row.title = @"手机号码";
        row.height = 30.f;
        [row.cellConfigAtConfigure setObject:@"请输入新的手机号码" forKey:@"rightTextField.placeholder"];
        [row.cellConfig setObject:self forKey:@"delegate"];
        [section addFormRow:row];
     
    //
    //    // 短信验证码
        row = [XLFormRowDescriptor formRowDescriptorWithTag:@"mobileCode" rowType:kInputInfoCellType];
        row.cellClass = [ECInputInfoCell class];
        row.title = @"短信验证码";
        row.height = 60.f;
        [row.cellConfigAtConfigure setObject:@"请输入验证码" forKey:@"rightTextField.placeholder"];
        
        [row.cellConfig setObject:self forKey:@"delegate"];
        [section addFormRow:row];
    
        // 登录密码
        row = [XLFormRowDescriptor formRowDescriptorWithTag:@"oldPwd" rowType:kInputInfoCellType];
        row.cellClass = [ECInputInfoCell class];
        row.title = @"登录密码";
        row.height = 60.f;
        [row.cellConfigAtConfigure setObject:@"请输入原登录密码" forKey:@"rightTextField.placeholder"];
        [row.cellConfig setObject:self forKey:@"delegate"];
        [section addFormRow:row];
        
        // 身份证号
        row = [XLFormRowDescriptor formRowDescriptorWithTag:@"cardNo" rowType:kInputInfoCellType];
        row.cellClass = [ECInputInfoCell class];
        row.title = @"身份证号";
        row.height = 60.f;
        [row.cellConfigAtConfigure setObject:@"请输入身份证号" forKey:@"rightTextField.placeholder"];
        [row.cellConfig setObject:self forKey:@"delegate"];
        [section addFormRow:row];
        
        self.form = form;
    }
    
    // MARK: - 方法监听
    
    /// 点击提交
    - (void)submitTapped:(UIButton *)sender {
        // 获取表单所有的值
        NSDictionary *values = [self formValues];
        NSLog(@"%@", values);
        
        NSString *phone = values[@"phone"]; // 手机号
        NSString *oldPwd = values[@"oldPwd"]; // 密码
        NSString *mobileCode = values[@"mobileCode"]; // 验证码
        NSString *cardNo = values[@"cardNo"]; // 身份证号
        
        if (phone.length == 0 || phone.length < 11) {
            [MBProgressHUD showTipMessageInWindow:@"请输入正确的手机号"];
        }else if (oldPwd.length == 0) {
            [MBProgressHUD showTipMessageInWindow:@"请输入登录密码"];
        }else if (oldPwd.length < 6) {
            [MBProgressHUD showTipMessageInWindow:@"密码错误"];
        }else if (mobileCode.length != 4) {
            [MBProgressHUD showTipMessageInWindow:@"请输入正确的验证码"];
        }else if (cardNo.length < 15) {
            [MBProgressHUD showTipMessageInWindow:@"请输入正确的身份证号"];
        }
        else{
            // 提交修改
            [self doModifyPhoneNumRequestWithUID:[ECUserSingleton shareInstance].getUserUid];
        }
    }
    /// 输入框中文字变化时调用
    - (void)ECInputInfoCell:(ECInputInfoCell *)cell textFieldEditingChanged:(UITextField *)textField {
        
    //    if (cell.rowDescriptor.title isEqualToString:@"")
        
    //    NSLog(@"正在输入: %@", textField.text);
    }
    /// 输入框输入完毕时调用，即释放第一响应者时
    - (void)ECInputInfoCell:(ECInputInfoCell *)cell textFieldDidEndEditing:(UITextField *)textField {
    //    NSLog(@"%@ 输入了: %@", cell.rowDescriptor.title,textField.text);
    }
    
    /// 点击获取验证码
    - (void)ECInputInfoCell:(ECInputInfoCell *)cell verifyCodeButtonTapped:(UIButton *)btn {
    
        WS(weakSelf);
        [self doSendCodeRequestPhone:self.formValues[@"phone"] type:9 uid:[ECUserSingleton shareInstance].getUserUid withCompletionBlock:^(BOOL isSuccess) {
            if (isSuccess) {
                // 按钮变灰，120s后恢复蓝色
                [weakSelf sentPhoneCodeTimeMethodWithButton:btn];
            }
        }];
        
    }
    
    /// 发送验证码
    - (void)doSendCodeRequestPhone:(NSString *)phoneNumber type:(NSInteger)type uid:(NSString *)uid withCompletionBlock:(void (^) (BOOL isSuccess))completionBlock{
        NSMutableDictionary *params = [NSMutableDictionary new];
        [params setValue:phoneNumber forKey:@"phone"];
        [params setValue:@(type) forKey:@"type"];
        
        _verifyCodeRequest = [[ECBaseRequest alloc]initWithinterfaceName:sendSmsInterFace andmethod:REQUEST_TYPE_POST andPhotos:nil andParams:params andResult:^(ECBaseResponse *response, NSError *error) {
            
            if (kRequestSuccess) {
                completionBlock(YES);
                [MBProgressHUD showTipMessageInWindow:[NSString stringWithFormat:@"验证码发送%@", response.msg]];
            }else {
                [MBProgressHUD showTipMessageInWindow:[NSString stringWithFormat:@"验证码发送%@", response.msg]];
            }
        }];
    }
     
    /// 提交进行手机修改
    - (void)doModifyPhoneNumRequestWithUID:(NSString *)uid {
        NSMutableDictionary *params = [[NSMutableDictionary alloc] initWithDictionary:self.formValues];
        
        // 取出密码
        NSString *oldPwd = params[@"oldPwd"]; // 密码
        // 加密后存入
        params[@"oldPwd"] = [oldPwd getRSAEncryptor]; // 存入加密后的密码
        
        _modifyPhoneNumRequest = [[ECBaseRequest alloc]initWithinterfaceName:modifyPhoneNumberWithID(uid) andmethod:REQUEST_TYPE_PUT andPhotos:nil andParams:params andResult:^(ECBaseResponse *response, NSError *error) {
            
            if (kRequestSuccess) {
                [MBProgressHUD showTipMessageInWindow:[NSString stringWithFormat:@"更改手机号%@", response.msg]];
                // 返回到主界面
                [self.navigationController popViewControllerAnimated:YES];
            }else {
                [MBProgressHUD showTipMessageInWindow:[NSString stringWithFormat:@"%@", response.msg]];
            }
        }];
    }
      
    
    - (void)sentPhoneCodeTimeMethodWithButton:(UIButton *)btn {
        //倒计时时间 - 120S
        __block NSInteger timeOut = 119;
        //执行队列
        dispatch_queue_t queue = dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0);
        //计时器 -》 dispatch_source_set_timer自动生成
        dispatch_source_t timer = dispatch_source_create(DISPATCH_SOURCE_TYPE_TIMER, 0, 0, queue);
        dispatch_source_set_timer(timer, DISPATCH_TIME_NOW, 1.0 * NSEC_PER_SEC, 0 * NSEC_PER_SEC);
        
        dispatch_source_set_event_handler(timer, ^{
            if (timeOut <= 0) {
                dispatch_source_cancel(timer);
                //主线程设置按钮样式
                dispatch_async(dispatch_get_main_queue(), ^{
                    // 倒计时结束
                    [btn setTitle:@"验证码" forState:UIControlStateNormal];
                    [btn setBackgroundColor:UIColorFromRGB(0x326EF0)];
                    [btn setUserInteractionEnabled:YES];
                });
            } else {
                //开始计时
                //剩余秒数 seconds
                NSInteger seconds = timeOut % 120;
                NSString *strTime = [NSString stringWithFormat:@"%.2lds", (long)seconds];
                //主线程设置按钮样式
                dispatch_async(dispatch_get_main_queue(), ^{
                    [UIView beginAnimations:nil context:nil];
                    [UIView setAnimationDuration:1.0];
                    
                    [btn setTitle:strTime forState:UIControlStateNormal];
                    [btn setBackgroundColor:CONSULTATION];
                    [btn setUserInteractionEnabled:NO];
                    
                    [UIView commitAnimations];
                    
                });
                timeOut--;
                
            }
        });
        dispatch_resume(timer);
    }
    
    // MARK: - 生命周期
    // MARK: - 数据源: 设置模型，展示数据
    // MARK: - 界面搭建
    // MARK: - 布局子控件
    // MARK: - 构造函数
    // MARK: - Getter: 属性懒加载
    
    - (void)viewDidLoad {
        [super viewDidLoad];
        self.tableView.backgroundColor = UIColor.whiteColor;
        self.tableView.separatorStyle = UITableViewCellSeparatorStyleNone;
    }
    
    
    
    - (UIView *)tableView:(UITableView *)tableView viewForHeaderInSection:(NSInteger)section {
        
        UIView *containerV = [UIView new];
        
        UILabel *lbl = [UILabel new];
        [containerV addSubview:lbl];
        lbl.text = @"更改手机号";
        lbl.font= FONT18;
        lbl.textColor = OWNER_HOMEVIEW_CELL_TITLE;
        
        [lbl mas_makeConstraints:^(MASConstraintMaker *make) {
            make.leading.mas_equalTo(30);
            make.top.bottom.trailing.mas_equalTo(0);
        }];
        
        return containerV;
    }
    
    - (CGFloat)tableView:(UITableView *)tableView heightForHeaderInSection:(NSInteger)section {
        return 80;
    }
    
    - (CGFloat)tableView:(UITableView *)tableView heightForFooterInSection:(NSInteger)section {
        return 74;
    }
    
    - (UIView *)tableView:(UITableView *)tableView viewForFooterInSection:(NSInteger)section {
        
        UIView *containerV = [UIView new];
        
        UIButton *btn = [UIButton new];
        [btn setTitle:@"提交" forState:UIControlStateNormal];
        [btn addTarget:self action:@selector(submitTapped:) forControlEvents:UIControlEventTouchUpInside];
        [containerV addSubview:btn];
        [btn mas_makeConstraints:^(MASConstraintMaker *make) {
            make.top.mas_equalTo(21);
            make.leading.mas_equalTo(30);
            make.trailing.mas_equalTo(-30);
            make.bottom.mas_equalTo(0);
        }];
        btn.backgroundColor = UIColorFromRGB(0x3C77FE);
        btn.layer.cornerRadius = 3.0;
        return containerV;
    }
    
    @end
    
    ```

    

