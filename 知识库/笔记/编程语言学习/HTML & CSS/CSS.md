# CSS

> 【详见Practice中的HTML练习】

- 简介

  > CSS的全称是Cascading Style Sheets，层叠样式表
  >
  > 用来控制HTML标签的样式，在美化网页中起到非常重要的作用

- CSS的编写格式是键值对形式的

  > color: red;
  >
  > background-color: blue;
  >
  > font-size: 20px;

- CSS有3种形式

  > 行内样式：直接在tag的属性处用style设置
  >
  > 页内样式: 创建一个style class，在tag属性处应用
  >
  > 外部样式: 在外部的css文件中声明style class，链接这个文件到此html，在tag属性处应用那些class

- 选择器

  - 作用

    > 选择对应的标签，为其添加样式

  - 分类

    > 标签选择器 div { color:red; }
    >
    > 类选择器 .cls { color:blue; }
    >
    > id选择器 #hi { color:orange; }
    >
    > 并列选择器 div, .cls { color: red; }【所有div和所有cls类都用这个样式】“或”
    >
    > 复合选择器 div .cls { color:red; }【是div且cls类的才用这个样式】"且"
    >
    > 后代选择器 div p {color: red;}
    >
    > 直接后代选择器 div > p {color: red;}

- 布局介绍

  > 【见practices中的布局介绍】

  