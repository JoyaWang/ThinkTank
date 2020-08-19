# The Linux Command Line

## INTRODUCTION

## PART I: LEARNING THE SHELL 学习Shell

### Chapter 1: What is the Shell? Shell是什么

#### 1. Terminal Emulators 终端仿真程序

#### 2. Making Your First Keystrokes

#### 3. Try Some Simple Commands

#### 4. Ending a Terminal Session

#### 5. Summing Up



### Chapter 2: Navigation 文件导航

#### 1. Understanding the File System Tree 理解文件系统树

#### 2. The Current Working Directory 当前工作文件夹

#### 3. Listing the Contents of a Directory 显示文件夹的文件目录

#### 4. Changing the Current Working Directory 切换当前工作文件夹

##### Absolute Pathnames 绝对路径名

##### Relative Pathnames 相对路径名

##### Some Helpful Shortcuts 有用的快捷键

#### Summing Up 总结



### Chapter 3: Exploring the System 探索文件系统

#### 1. More Fun with ls ls的更多用法

##### 	Options and Arguments 选项和参数？

##### 	A Longer Look at Long Format 长格式

#### 2. Determing a File's Type with file 使用file命令查看一个文件的类型

#### 3. Viewing File Contents with less 使用less命令查看文件内容

#### 4. Taking a Guided Tour 

#### 5. Symbolic Links

#### 6. Hard Links

#### 7. Summing Up 总结



### Chapter 4: Manipulating Files and Dictionaries 操作文件和字典

#### 1. Wildcards 通配符

#### 2. mkdir - Create Directories 创建文件夹

#### 3. cp - Copy Files and Directories 复制文件和文件夹

#### 4. mv - Move and Rename Files 移动和重命名文件

#### 5. rm - Remove files and Directories 删除文件和文件夹

#### 6. ln - Create Links 创建链接

#### 7. Building a Playground

##### Creating Directories

##### Copying Files

##### Moving and Renaming Files

##### Creating Symbolic Links

##### Removing Files and Directories



### Chapter 5: Working with Commands 使用命令

#### 1. What Exactly Are Commands? 命令到底是什么？

#### 2. Identifying Commands 辨别命令

##### type - Display a Command's Type 显示命令的类别

##### which - Display an Executable's Location 显示可执行命令的位置

#### 3. Getting a Command's Documentation 获取命令的文档

##### help - Get Help for Shell Builtins 获取Shell内置命令的帮助

##### --help - Display Usage Information 显示使用信息

##### man - Display a Program's Manual Page 显示一个程序的使用手册页

##### apropos - Display Appropriate Commands 显示合适的命令?

##### whatis - Display One-line Manual Page Description 显示一行手册页描述

##### info - Display a Program's Info Entry 显示一个程序信息入口

##### README and Other Program Documentation Files README和其他程序文档文件

#### 4. Creating Our Own Commands with alias 用快捷方式创建我们自己的命令

#### 5. Summing Up 总结



### Chapter 6: Redirection 重定向

#### 1. Standard Input, Output, and Error 标准输入、输出和错误

#### 2. Redirecting Standard Output 重定向标准输出

#### 3. Redirecting Standard Error 重定向标准错误

##### Redirecting Standard Output and Standard Error to One File 将标准输出和标准错误重定向到一个文件

##### Disposing of Unwanted Output 处理不想要的输出

#### 4. Redirecting Standard Input 重定向标准输出

##### cat: Concatenate Files cat命令连结文件

#### 5. Pipelines

##### Filters 过滤

##### uniq: Report or Omit Repeated Lines 报告或者忽略重复行

##### wc: Print Line, Word, and Byte Counts 打印行、单词和字节数

##### grep: Print Lines Matching a Pattern 打印匹配一个模式的行

##### head/tail: Print First/Last Part of Files 打印文件的头/尾部

##### tee: Read from Stdin and Output to Stdout and Files 从标准输入读取并输出到标准输出和文件



### Chapter 7: Seeing the World as the Shell Sees It

#### 1. Expansion 扩展？

##### Pathname Expansion 路径名扩展?

##### Tilde Expansion

##### Arithmetic Expansion 算术扩展？

##### Brace Expansion

##### Parameter Expansion 参数扩展

##### Command Substitution 命令替换

#### 2. Quoting

##### Double Quotes

##### Single Quote

##### Escaping Characters 

##### Backslash Escape Sequences

#### 3. Summing Up



### Chapter 8: Advanced Keyboard Tricks

#### 1. Command Line Editing 命令行编辑

##### Cursor Movement 光标移动

##### Modifying Text 修改文字

##### Cutting and Pasting (Killing and Yanking) Text 剪切和粘贴

#### 2. Completion 补全

#### 3. Using History 使用历史

##### Searching History 搜索历史

##### History Expansion 历史扩展?

#### 4. Summing Up



### Chapter 9: Permissions

#### 1. Owners, Group Members, and Everybody Else 拥有者、群组成员、其他人

#### 2. Reading，Writing，and Executing 读取、写入和执行

##### chmod: Change File Mode 修改文件模式

##### Setting File Mode with the GUI 使用GUI修改文件模式

##### umask: Set Default Permissions 设置默认权限

##### Some Special Permission 一些特殊权限

#### 3. Changing Identities

##### su: Run a Shell with Substitute User and Group IDs 更换用户

##### sudo: Execute a Command As Another User 

##### chown: Change File Owner and Group 改变文件所有者和所属群组

##### chgrp: Change Group Ownership 更改群组

#### 4. Exercising Our Privileges

#### 5. Changing Your Password

#### 6. Summing Up



### Chapter 10: Processes

#### 1. How a Process Works 一个程序怎么工作

#### 2. Viewing Processes 查看程序

##### Viewing Processes Dynamically with top 使用top命令动态查看所有程序

#### 3. Controlling Processes 控制程序

##### Interrupting a Process 中断一个程序

##### Putting a Process in the Background 将一个程序放到后台

##### Returning a Process to the Foreground 将程序返回到前台

##### Stopping (Pausing) a Process 停止(暂停)一个程序

#### 4. Signals

##### Sending Signals to Processes with kill 使用kill命令向程序发送信号

##### Sending Signals to Multiple Processes with killall 使用killall命令向多个程序发送信号

#### 5. Shutting Down the System 关闭系统

#### 6. More Process-Related Commands 更多程序相关的命令

#### 7. Summing Up 总结



## PART II: CONFIGURATION AND THE ENVIRONMENT 配置和环境

### Chapter 11: The Environment 环境

#### 1. What is Stored in the Environment? 环境中存储了什么？

##### Examining the Environment 检查环境

##### Some Interesting Variables 一些有趣的变量

#### 2. How is the Environmnet Established 环境是怎么建立的？

##### What's in a Startup File? 启动文件中有什么？

#### 3. Modifying the Environment 修改环境

##### Which Files Should We Modify? 我们应该修改哪些文件？

##### Text Editors 文件编辑器

##### Using a Text Editor 使用文件编辑器

##### Activating Our Changing 激活我们的更改

### Chapter 12: A Gentle Introduction to vi 简单介绍vi编辑器

#### 1. Why We should Learn Vi 为什么要使用Vi

#### 2. A Little Background 背景

#### 3. Starting and Stopping vi 使用和停止vi

#### 4. Editing Modes 编辑模式

##### Entering Insert Mode 进入插入模式

##### Saving Our Work 保存我们的工作

#### 5. Moving the Cursor Around 移动光标

#### 6. Basic Editing 基本编辑

##### Appending Text 添加文字

##### Opening a Line 开启一行

##### Deleting Text 删除文字

##### Cutting, Copying, and Pasting Text 剪切、复制和粘贴

##### Joining Lines 拼接行

#### 7. Searching and Replace 搜索和替换

##### Searching Within a Line 行内搜索

##### Searching the Entire File 在整个文件中搜索

##### Global Search-and-Replace 全局搜索和替换

#### 8. Editing Multiple Files 编辑多个文件

##### Switching Between Files 切换文件

##### Opening Additional Files for Editing 打开多个文件进行编辑

##### Copying Content from One File into Another 从一个文件中粘贴内容到另一个

##### Inserting an Entire File into Another 将整个文件插入到另一个中

#### 9. Saving Our Work 保存

#### 10. Summing Up 总结

### Chapter 13: Customizing the Prompt

#### 1. Anatomy of a Prompt

#### 2. Trying Some Alternative Prompt Designs

#### 3. Adding Color

#### 4. Moving the Cursor

#### 5. Saving the Prompt

#### 6. Summing Up

## PART III: COMMON TASKS AND ESSENTIALS TOOLS 普通任务和基本工具

### Chapter 14: Package Management 包管理

#### 1. Packaging Systems 打包系统

#### 2. How a Package System Works 包系统怎么工作

##### Package Files 包文件

##### Repositories 库

##### Dependencies 依赖

##### High- and Low-Level Package Tools 高级和低级打包工具

#### 3. Common Package Management Tasks 普通包管理任务

##### Finding a Package in a Repository 从库中寻找包

##### Installing a Package from a Repository 从库中安装包

##### Installing a Package from a Package File 从包文件中安装包

##### Removing a Package 删除包

##### Updating Packages from a Repository 从库中更新包

##### Updating a Package from a Package File 从包文件中更新包

##### Listing Installed Packages 显示所有安装的包

##### Determining Whether a Package Is Installed 查看是否安装了某个包

##### Displaying Information About an Installed Package 显示一个已安装的包的信息

##### Finding Which Package Installed a File 查找哪个包安装了文件

#### 4. Summing Up



### Chapter 15: Storage Media 存储介质

#### 1. Mounting and Unmounting Storage Devices 加载和推出存储设备

##### Viewing a List of Mounted File Systems 查看加载的文件系统列表

##### Determining Device Names 决定设备名称

#### 2. Creating New File System 创建新文件系统

##### Manipulating Partitions with fdisk 用fdisk命令进行分区

##### Creating a New File System with mkfs 用mkfs命令创建一个新文件系统

#### 3. Testing and Repairing File Systems 测试和修复文件系统

#### 4. Moving Data Directly to and from Devices 设备间移动数据

##### Creating CD-ROM Images 创建CD-ROM镜像?

##### Creating an Image Copy of a CD-ROM 创建镜像复件

##### Creating an Image from a Collection of Files 用文件集合创建镜像

#### 5. Writing CD-ROM Images 写入镜像

##### Mounting an ISO Image Directly 直接加载一个ISO镜像

##### Blanking a Rewritable CD-ROM 清空一个可重复读写的CD-ROM

##### Writing an Image 写入一个镜像

#### 6. Summing Up

#### 7. Extra Credit



### Chapter 16: Networking 网络

#### 1. Examining and Monitoring a Network 检查和监控一个网络

##### ping 

##### traceroute

##### ip

##### netstat

#### 2. Transporting Files over a Network 通过网络传输文件

##### ftp

##### lftp-a Better ftp

##### wget

#### 3. Secure Communication with Remote Hosts 与远程主机间安全通信

##### ssh

##### scp and sftp

#### 4. Summing Up



### Chapter 17: Searching for Files 搜索查找文件

#### 1. locate-Find Files the Easy Way 

#### 2. find - Find Files the Hard Way

##### Tests

##### Operators

##### Predefined Actions

##### Improving Efficiency

##### xargs

##### A Return to the Playground

##### find Options

#### 3. Summing Up



### Chapter 18: Archiving and Backup 归档和备份

#### 1. Compressing Files 压缩文件

##### gzip

##### bzip2

#### 2. Archiving Files 归档文件

##### tar

##### zip

#### 3. Synchronizing Files and Directories 同步文件和文件夹

##### Using rsync over a Network

#### 4. Summing Up



### Chapter 19: Regular Expressions 正则表达式

#### 1. What Are Regular Expressions? 正则表达式是什么

#### 2. grep

#### 3. Metacharacters and Literals 

#### 4. The Any Character

#### 5. Anchors

#### 6. Bracket Expressions and Character Ranges

##### Negation

##### Traditional Character Ranges

#### 7. POSIX Character Classes

#### 8. POSIX Basic vs. Extended Regular Expressions

#### 9. Alternation

#### 10. Quantifiers

##### ? - Match an Element Zero or One Time

##### *- Match an Element Zero or More Times

##### +- Match an Element One or More Times

##### { }- Match an Element a Specific Number of Times

#### 11. Putting Regular Expressions to Work

##### Validating a Phone List with grep

##### Finding Ugly Filenames with find

##### Searching for Files with locate

##### Searching for Text with less and vim

#### 12. Summing Up



### Chapter 20: Text Processing 文字处理

#### 1. Applications of Text 文字的应用

##### Documents 文件

##### Web Pages 网页

##### Email 邮件

##### Printer Output 打印机输出

##### Program Source Code 程序源码

#### 2. Revisiting Some Old Friends

##### cat

##### sort

##### uniq

#### 3. Slicing and Dicing 

##### cut - Remove Sections from Each Line of Files 剪切 - 从每行中删除一部分

##### paste - Merge Lines of Files 粘贴 - 合并文件中的行

##### join - Join Lines of Two Files on a Common Field 拼接

#### 4. Comparing Text

comm - Compare Two Sorted Files Line by line

diff - Compare Files line by line

patch - Apply a diff to an Original

#### 5. Editing on the Fly

tr - Transliterate or Delete Characters

sed - Stream Editor for Filtering and Transforming Text

aspell - Interactive Spellchecker

#### 6. Summing Up

#### 7. Extra Credit



### Chapter 21: Formatting Output 格式化输出

#### 1. Simple Formatting Tools 简单的格式化工具

##### nl - Number Lines 

##### fold - Wrap Each Line to a Specified Length

##### fmt - A Simple Text Formatter

##### pr - Format Text for Printing

##### printf - Format and Print Data

#### 2. Document Formatting Systems 文件格式化系统

##### groff



### Chapter 22: Printing

#### 1. A Brief History of Printing

##### Printing in the Dim Times

##### Character-Based Printers 基于character的打印机

##### Graphical Printers 图像打印机

#### 2. Printing with Linux 在Linux中打印

#### 3. Preparing Files for Printing 准备要打印的文件

pr - Convert Text Files for Printing 转换文字文件以打印

#### 4. Sending a Print Job to a Printer 向打印机发送一个打印任务

lpr - Print Files (Berkeley Style)

lp - Print Files (System V Style)

Another Option: a2ps

#### 5. Monitering and Controlling Print Jobs 监视和控制打印任务

lpstat - Display Print System Status 显示打印系统状态

lpq - Display Printer Queue Status 显示打印机队列状态

lprm/cancel - Cancel Print Jobs 取消打印任务

#### 6. Summing Up



### Chapter 23: Compiling Programs 编译程序

#### 1. What is Compiling? 什么是编译？

Are all Programs Compiled?

#### 2. Compiling a C Program 编译一个C程序

Obtaining the Source Code 获取源码

Examining the Source Tree 检查源树？

Building the Program 构建程序

Installing the Program 安装程序

#### 3. Summing Up



## PART IV:  WRITING SHELL SCRIPTS 编写Shell脚本

### Chapter 24: Writing Your First Scripts

#### 1. What Are Shell Scripts? 什么是Shell脚本

#### 2. How to Write a Shell Script? 

Script File Format 脚本文件格式

Executable Permissions 可执行权限

Script File Location 脚本文件位置

Good Locations for Scripts 好的脚本文件位置

#### 3. More Formatting Tricks 更多格式技巧

Long Option Names 长选项名称

Indentation and Line Continuation 缩进和行继续

#### 4. Summing Up



### Chapter 25: Starting a Project 开始一个项目

#### 1. First Stage: Minimal Document 

#### 2. Second Stage: Adding a Little Data

#### 3. Variables and Constants 变量和常量

Assigning Values to Variables and Constants 向变量和常量赋值

#### 4. Here Documents

#### 5. Summing Up



### Chapter 26: Top-Down Design

#### 1. Shell  Functions Shell函数

#### 2. Local Variables 局部变量

#### 3. Keep Scripts Running 保持脚本运行

#### 4. Summing Up



### Chapter 27: Flow Control: Branching with If

#### 1. if Statements if语句

#### 2. Exit Status 退出状态

#### 3. Using test 使用test

File Expressions

String Expressions

Integer Expressions

#### 4. A More Modern Version of Test

#### 5. (()) - Designed for Integers

#### 6. Combining Expressions 结合表达式

#### 7. Control Operators: Another Way to Branch 控制操作符: 分支的另一种方式

#### 8. Summing Up



### Chapter 28: Reading Keyboard Input 读取键盘输入

#### 1. read - Read Values from Standard Input 从标准输入中读取数值

#### 2. Validating Input 验证输入

#### 3. Menus

#### 4. Summing Up

#### 5. Extra Credit



### Chapter 29: Flow Control: Looping with while/until 流控制: 使用while和until循环

#### 1. Looping 循环

while

#### 2. Breaking Out of a Loop 终止循环

until

#### 3. Reading Files with Loops 使用循环读取文件

#### 4. Summing Up



### Chapter 30: Troubleshooting 常见问题

#### 1. Syntactic Errors 语法错误

Missing Quotes

Missing or Unexpected Tokens

Unanticipated Expansions

#### 2. Logical Errors 逻辑错误

Defensive Programming

Watch out for Filenames 注意文件名

Verifying Input 验证输入

#### 3. Testing 测试

Test Case 测试用例

#### 4. Debugging

Finding the Problem Area 查找问题区域

Tracing 追踪

Examining Values  During Execution 在执行过程中检查值

#### 5. Summing Up



### Chapter 31: Flow Control: Branching with case 流控制: 使用case进行分支

#### 1. The case Command

Patterns

Performing Multiple Actions 执行多个动作

#### 2. Summing Up



### Chapter 32: Positional Parameters 

#### 1. Accessing the Command Line 

Determining the Number of Arguments

shift - Getting Access to Many Arguments

Simple Applications 

Using Positional Parameters with Shell Functions

#### 2. Handling Positional Parametes en Masse

#### 3. A More Complete Application

#### 4. Summing Up



### Chapter 33: Flow Control: Looping with for 流控制: 用for进行循环

#### 1. for: Traditional Shell Form

#### 2. for: C Language Form

#### 3. Summing Up



### Chapter 34: Strings and Numbers 字符串和数字

#### 1. Parameter Expansion

Basic Parameters

Expansions to Manage Empty Variables

Expansions That Return Variable Names

String Operations

Case Conversion

#### 2. Arithmetic Evaluation and Expansion

Number Bases

Unary Operators

Simple Arithmatic

Assignment

Bit Operations

Logic

#### 3. bc - An Arbitrary Precision Calculator Language

Using bc

An Example Script

#### 4. Summing Up

#### 5. Extra Credit



### Chapter 35: Arrays 数组

#### 1. What Are Arrays? 什么是数组?

#### 2. Creating an Array 创建一个数组

#### 3. Assigning Values to an Array 往数组中添加数值

#### 4. Accessing Array Elements 获取数组中的元素

#### 5. Array Operations 数组操作

Outputing the Entire Contents of an Array 输出数组的所有内容

Determining the Number of Array Elements 确定数组元素数量

Finding the Subscripts Used by an Array 找出数组使用的下标

Adding Elements to the End of an Array 向数组后面添加元素

Sorting an Array 排序一个数组

Deleting an Array 删除一个数组

#### 6. Associative Arrays

#### 7. Summing Up



### Chapter 36: Exotica

#### 1. Group Commands and Subshells

Process Substitution

#### 2. Traps

#### 3. Asynchronous Execution with wait

#### 4. Named Pipes

Setting Up a Named Pipe

Using Named Pipes

#### 5. Summing Up

### Index