# Shell

## 编写脚本文件

**#!/bin/sh**，它同样也可以改为 **#!/bin/bash**。

**#!** 告诉系统其后路径所指定的程序即是解释此脚本文件的 Shell 程序。

```shell
#!/bin/bash
echo "Hello World !"
```

echo 命令用于向窗口输出文本。



## 运行 Shell 脚本有两种方法：

**1、作为可执行程序**

将上面的代码保存为 test.sh，并 cd 到相应目录：

```
chmod +x ./test.sh  #使脚本具有执行权限
./test.sh  #执行脚本
```

注意，一定要写成 **./test.sh**，而不是 **test.sh**，运行其它二进制的程序也一样，直接写 test.sh，linux 系统会去 PATH 里寻找有没有叫 test.sh 的，而只有 /bin, /sbin, /usr/bin，/usr/sbin 等在 PATH 里，你的当前目录通常不在 PATH 里，所以写成 test.sh 是会找不到命令的，要用 ./test.sh 告诉系统说，就在当前目录找。

**2、作为解释器参数**

这种运行方式是，直接运行解释器，其参数就是 shell 脚本的文件名，如：

```
/bin/sh test.sh
/bin/php test.php
```

这种方式运行的脚本，不需要在第一行指定解释器信息，写了也没用。



## Shell 变量

### 定义变量

```shell
your_name="runoob.com"
```

### 使用变量

```shell
your_name="qinjx"
echo $your_name
echo ${your_name}
```

### 只读变量

```shell
#!/bin/bash
myUrl="https://www.google.com"
readonly myUrl
myUrl="https://www.runoob.com"
```

### 删除变量

```shell
unset variable_name
```

### 变量类型

运行shell时，会同时存在三种变量：

- **1) 局部变量** 局部变量在脚本或命令中定义，仅在当前shell实例中有效，其他shell启动的程序不能访问局部变量。
- **2) 环境变量** 所有的程序，包括shell启动的程序，都能访问环境变量，有些程序需要环境变量来保证其正常运行。必要的时候shell脚本也可以定义环境变量。
- **3) shell变量** shell变量是由shell程序设置的特殊变量。shell变量中有一部分是环境变量，有一部分是局部变量，这些变量保证了shell的正常运行

## Shell字符串

```shell
# 声明变量
str='Hello'
# 声明变量
your_name='Lebron'
# 拼接字符串并输出
echo "${str}, ${your_name}, nice to see you here!"



#获取字符串长度
string="abcd"
echo "string字符串的长度为:${#string}"

#提取字符串
str0="ThinkTank is a greate site"
echo ${str0:1:4} #打印出字符串1-4位的文字

#查找字符串 貌似有问题
echo `expr index "$str0" io`
```

## 数组

```shell
#!/bin/bash

# 定义数组
array_name=("Joya" "Alice" "JoeyZoey" "YY")

# 读取数组
name1=${array_name[0]}

echo "第一个名字是: ${name1}"

# 用@或*获取数组中的所有元素
echo "所有名字是: ${array_name[@]}"

# 获取数组长度
length0=${#array_name[@]}
echo "array_name数组元素数量为${length0}"
# 或者
length1=${#array_name[*]}
echo "array_name数组元素数量为${length1}"

# 取得数组单个元素的长度
length2=${#array_name[2]}
echo "数组中第三个元素的长度为${length2}"
```

## 注释

以 **#** 开头的行就是注释，会被解释器忽略。

通过每一行加一个 **#** 号设置多行注释，像这样：

```
#--------------------------------------------
# 这是一个注释
# author：菜鸟教程
# site：www.runoob.com
# slogan：学的不仅是技术，更是梦想！
#--------------------------------------------
##### 用户配置区 开始 #####
#
#
# 这里可以添加脚本描述信息
# 
#
##### 用户配置区 结束  #####
```

如果在开发过程中，遇到大段的代码需要临时注释起来，过一会儿又取消注释，怎么办呢？

每一行加个#符号太费力了，可以把这一段要注释的代码用一对花括号括起来，定义成一个函数，没有地方调用这个函数，这块代码就不会执行，达到了和注释一样的效果。

### 多行注释

多行注释还可以使用以下格式：

```shell
:<<EOF
注释内容...
注释内容...
注释内容...
EOF
```

EOF 也可以使用其他符号:

```shell
:<<'
注释内容...
注释内容...
注释内容...
'

:<<!
注释内容...
注释内容...
注释内容...
!
```

## 向shell脚本传递参数

- 创建名为 接收参数的脚本.sh 的脚本文件

```
#!/bin/sh

echo "shell传递参数实例"

echo "执行的文件名为 $0";
echo "接收到的第1个参数为: $1";
echo "接收到的第2个参数为: $2";
echo "接收到的第3个参数为: $3";
```

- 执行脚本文件并传参

```
/bin/sh 接收参数的脚本.sh Joya is Here
```



## 运算符

```shell
#! /bin/bash

echo "--------------算术运算----------------"
# 加法计算
val=`expr 2 + 2`
echo "两数之和为: ${val}"

# 算术运算
a=10
b=20

# 加法 
val0=`expr $a + $b`
echo "a + b 等于 $val"

# 减法
val1=`expr $a - $b`
echo "a - b 等于 $val1"

# 乘法
val2=`expr $a \* $b`
echo "a * b 等于 $val2"

# 除法
val3=`expr $b / $a`
echo "b / a 等于 $val3"

# 取余
val4=`expr $b % $a`
echo "b 取余 a 等于$val4"


echo "--------------条件判断----------------"
# 条件判断
if [ $a == $b ]
then
echo "a 等于 b"
fi

if [ $a != $b ] 
then
echo "a 不等于 b"
fi

echo "--------------关系运算符----------------"
# 关系运算符
# 等于 equal
if [ $a -eq $b ]
then 
echo "$a -eq $b : a 等于 b"
else
echo "$a -eq $b: a 不等于 b"
fi

# 不等于 not equal
if [ $a -ne $b ]
then
echo "$a -ne $b: a 不等于 b"
else
echo "$a -ne $b: a 等于 b"
fi

# 大于 greater than
if [ $a -gt $b ]
then
echo "$a -gt $b: a 大于 b"
else
echo "$a -gt $b: a 不大于 b"
fi

# 小于 less than
if [ $a -lt $b ]
then
echo "$a -lt $b: a 小于 b"
else
echo "$a -lt $b: a 不小于 b"
fi

# 大于等于 greaterThanOrEqualTo
if [ $a -ge $b ]
then
echo "$a -ge $b: a 大于或等于 b"
else
echo "$a -ge $b: a 小于 b"
fi


# 小于等于 lessThanOrEqualTo
if [ $a -le $b ]
then 
echo "$a -le $b: a 小于或等于 b"
else
echo "$a -le $b: a 大于 b"
fi

echo "--------------逻辑运算：且、或----------------"
# 逻辑运算符 且、或
if [[ $a -lt 100 && $b -gt 100 ]]
then
echo "$a 小于100并且$b 大于100"
else
echo "$a 不小于100或$b 不大于100"
fi

if [[ $a -lt 100 || $b -gt 100 ]]
then
echo "$a 小于100或者$b 大于100"
else
echo "$a 不小于100且$b 不大于100"
fi


echo "--------------字符串判断----------------"
# 声明两个字符串变量
c="abc"
d="efg"

if [ $c = $d ]
then
echo "$c = $d : c 等于 d"
else
echo "$c = $d : c 不等于 d"
fi

if [ $c != $d ]
then
echo "$c != $d : c 不等于 d"
else
echo "$c != $d : c 等于 d"
fi

if [ -z $c ]
then
echo "-z $c : 字符串长度为 0"
else
echo "-z $c : 字符串长度不为 0"
fi

if [ -n "$c" ]
then 
echo "-n $c : 字符串长度不为 0"
else
echo "-n $c : 字符串长度为 0"
fi

if [ $c ]
then
echo "$c : 字符串不为空"
else
echo "$c : 字符串为空"
fi

echo "--------------文件测试运算符----------------"

file="/Users/joyawang/Desktop/Shell Scripts/test.sh"

if [[ -r ${file} ]]
then 
echo "文件可读"
else
echo "文件不可读"
fi

if [ -w "$file" ]
then 
echo "文件可写"
else
echo "文件不可写"
fi

if [[ -x $file ]]
then
echo "文件可执行"
else
echo "文件不可执行"
fi

if [[ -f $file ]]
then
echo "文件为普通文件"
else
echo "文件为特殊文件"
fi

if [ -d "$file" ]
then
echo "文件是个目录"
else
echo "文件不是目录"
fi

if [ -s "$file" ]
then
echo "文件不为空"
else
echo "文件为空"
fi

if [ -e "$file" ]
then
echo "文件存在"
else 
echo "文件不存在"
fi

```



## 流程控制

### if else

### for 循环

### while 语句

### 无限循环

### until 循环

### case

### 跳出循环

- break命令
- continue
- case ... esac



## 函数

```shell
#! /bin/bash

# 普通函数
demoFunc() {
 echo "这是我的第一个 shell 函数"
}

echo "---开始执行函数---"

demoFunc

echo "---函数执行完毕---"

# 带return返回值的函数
funcWithReturn() {
 echo "这个函数会对输入的两个数字进行相加运算..."
 echo "第一个数字: "
 read aNum # 从控制台读取用户输入
 echo "输入第二个数字: "
 read anotherNum
 echo "两个数字分别为 $aNum 和 $anotherNum !"
 return $(($aNum+$anotherNum))
}
funcWithReturn # 调用函数
echo "输入的两个数字之和为: $? !" # 函数返回值在调用该函数后通过 $? 来获得

# 带参数的函数
funcWithParam() {
 echo "第一个参数为 $1 !"
 echo "第二个参数为 $2 !"
 echo "第10个参数为 $10 !"
 echo "第10个参数为 ${10} !"
 echo "第11个参数为 ${11} !"
 echo "参数总数有 $# 个！"
 echo "作为一个字符串输出所有参数 $* !"
}
funcWithParam 1 2 3 4 5 6 7 8 9 34 23 # 调用函数，传入参数

```

## 搜索

- 寻找特定文件夹下以.a结尾的文件

  ```
  find /Users/joyawang/Library/Developer/Xcode/DerivedData/Build/Products/Debug-iphoneos -name "*.a"
  ```

- 在/home目录下查找以.txt结尾的文件名

  ```
  find /home -name "*.txt"
  ```

- 同上，但忽略大小写

  ```
  find /home -iname "*.txt"
  ```

- ```shell
  #!/bin/bash
  
  
  # 打印目录下所有文件夹和文件名称recursive
  function echo_name(){ 
      for file in `ls $1`
          do
              echo $1"/"$file
              if [ -d $1"/"$file ]
              then
                  echo_name $1"/"$file
              fi
          done
  } 
  
  # 调用函数并传递一个文件夹路径
  # echo_name /Users/joyawang/Library/Developer/Xcode/DerivedData/Build/Products/Debug-iphoneos
  
  # 获取指定路径的文件夹内包含特定名称的文件
  # 声明一个空数组
  results=()
  function getAllFileNames {
  
      # 遍历文件夹
      i=0
      # 搜索条件
      str=".a"
      # $1指传进来的第一个参数，也就是那个指定的文件夹路径
      for file in `ls $1`
      do
      # 如果数组元素名包含.a
      if [[ $1/${file} == *$str ]]
      then
      # 保存到数组
      results[${#results[@]}]=$1"/"$file
      fi
  
      # 如果数组元素是文件夹
      if [ -d $1"/"$file ]
      then
      # 递归
      getAllFileNames $1"/"$file
      fi
      done
  }
  
  # 调用函数并传递参数
  getAllFileNames /Users/joyawang/Library/Developer/Xcode/DerivedData/Build/Products/Debug-iphoneos
  
  # 要被替换掉的部分
  str1="/Users/joyawang/Library/Developer/Xcode/DerivedData/Build/Products/Debug-iphoneos"
  # 用来替换的部分
  str2="-force_load \$(BUILT_PRODUCTS_DIR)"
  
  # 把数组中的文件名全部替换并打印出来
  for res in ${results[@]}
      do
          # 将字符串中的str1替换为str2后，打印出来
          echo ${res/$str1/$str2}
      done
  
  
  ```

  

