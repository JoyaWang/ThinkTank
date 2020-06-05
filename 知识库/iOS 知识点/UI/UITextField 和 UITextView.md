# UITextField 和 UITextView

## UITextField

监听输入框的状态

- 在第一次点击文本框准备进行输入时调用 textFieldShouldBeginEditing 【UITextFieldDelegate】

  > 只在第一次点击文本框准备进行输入时调用，设置文本框是否能够被编辑，No的话，里面的文字不能被编辑

- 文本框已经开始编辑(成为第一响应者后) textFieldDidBeginEditing【UITextFieldDelegate】

- 是否允许此文本框结束编辑(是否允许它释放第一响应者) textFieldShouldEndEditing【UITextFieldDelegate】

- 文本框已经结束编辑(已经释放第一响应者) textFieldDidEndEditing【UITextFieldDelegate】

- 是否允许可以改动文本框中的内容 textFieldShouldChangeCharactersInRange: replacementString:【UITextFieldDelegate】

- 监听键盘回车键被点击时调用 textFieldShouldReturn【UITextFieldDelegate】

- 监听键盘中文字的变动，用户实时输入，这里实时调用

  > 用add Target 监听 UIControlEventEditingChanged 事件
  >
  > ```
  > [_rightTextField addTarget:self action:@selector(textFieldValueDidChanged:) forControlEvents:UIControlEventEditingChanged];
  > ```

### 退出键盘

* 释放第一响应者
  第一响应者：能够叫出键盘的控件，可以切换
  [textField resignFirstResponder]
* 结束可能成为第一响应者的控件的父控件的编辑状态
  [self.view endEditing:YES]



- 判断文本视图是否有文字 hasText
- 输入视图 inputView 通常设置一个 toolBar
- 输入助理视图 inputAccessoryView 
- textView.reloadInputViews() 切换键盘视图一定要刷新，否则不成功