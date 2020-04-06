# iOS 中的使用

- URL 正则表达式 Pattern
  
  ```swift
  let urlPattern = "[a-zA-Z]*://[a-zA-Z0-9/\\.]*"
  ```
  
  
  
- 正则表达式常用选项

  - `CaseInsensitive` 忽略大小写
  - `DotMatchesLineSeparators` `.` 匹配换行符

- 匹配方案
  - `.` 匹配任意字符
  - `*` 匹配 0~ 任意 多个字符
  - `?` 尽可能少的重复

- 匹配函数
  - `matchesInString`
    - 重复匹配多次 `pattern`
    - 如果匹配成功，生成 `NSTextCheckingResult` 数组
  - `firstMatchesInString`
    - 匹配第一个 pattern
    - 如果匹配成功，生成 `NSTextCheckingResult`

- 匹配结果
  - `numberOfRanges`
    - 匹配的 `range` 计数
    - 如果匹配成功，是 `()` 的数量 `+ 1`
  - `rangeAtIndex`

