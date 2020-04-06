# iOS 中的 URL 类

> meituan:///showP1:P2:P3:P4:/大西瓜/红牛/小樱桃/小肥羊

- 属性
  - scheme 协议头

    > meituan

  - host 主机头

    > nil
    >
    > 如果没有 ///

  - pathComponents

    > 返回数组
    >
    > URL 中所有路径的数组
    >
    > `show：P1:P2:P3:P4:`
    >
    > - 大西瓜
    > - 红牛
    > - 小樱桃
    > - 小肥羊

  - query 查询字符串

    > URL  中 ? 后面所有的内容



