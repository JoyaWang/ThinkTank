# UI 界面间 传值

> 如果要传的值有2个以上，封装数据模型传送

- ### 传值方式

  > - 顺传值
  >
  >   - Storyboard 拖线的话，prepareForSegue 
  >   - 手动 push 或 present 的话，在当时传
  >
  > - 逆传值
  >
  >   - 代理模式
  >
  >     > 一对一，代理只能设置一次，如多次设置，只最后一次设置的起作用
  >
  >   - block / closure
  >
  >     > 实例：私人通讯录_新建修改
  >
  >   - 通知
  >
  >     > 一对多
  >
  >   - AddTarget

