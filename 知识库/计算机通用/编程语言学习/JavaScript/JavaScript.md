# JavaScript

- ### 介绍

  > JavaScript是一门广泛用于浏览器客户端的脚本语言
  >
  > 由Netspace公司设计，当时跟Sun公司合作，所以名字起的像Java
  >
  > 一般简称JS

- ### 常见用途

  > HTML DOM操作(节点操作，比如添加、修改、删除节点)
  >
  > 给HTML网页增加动态功能，比如动画
  >
  > 事件处理：比如监听鼠标点击、鼠标滑动、键盘输入

- ### 语法
  - 声明变量

    > var num = 5;

  - 循环

    ```js
    for (var i = 0; i < 5; i++) {
    
    }
    ```

  - 打印到控制台

    ```js
    console.log()
    ```

  - 声明方法

    ```js
    function() {
    }
    ```

    

  - 获取HTML文档中的控件

    ```js
    document.getElementById("textField1"); 
    
    document.getElementsByTagName("input"); 返回数组
    ```

    

  - 判断

  - viewDidLoad

    ```js
    window.onload = function() {当html的所有view全都加载完毕后执行的代码}
    ```

  - 跳转到文档中的某个位置

    ```js
    document.location.href = '#id号';
    ```

    

