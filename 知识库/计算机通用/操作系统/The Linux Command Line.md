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

## PART III: COMMON TASKS AND ESSENTIALS TOOLS

### Chapter 14: Package Management

### Chapter 15: Storage Media

### Chapter 16: Networking

### Chapter 17: Searching for Files

### Chapter 18: Archiving and Backup

### Chapter 19: Regular Expressions

### Chapter 20: Text Processing

### Chapter 21: Formatting Output

### Chapter 22: Printing

### Chapter 23: Compiling Programs



## PART IV:  WRITING SHELL SCRIPTS

### Chapter 24: Writing Your First Scripts

### Chapter 25: Starting a Project

### Chapter 26: Top-Down Design

### Chapter 27: Flow Control: Branching with If

### Chapter 28: Reading Keyboard Input

### Chapter 29: Flow Control: Looping with while/until

### Chapter 30: Troubleshooting

### Chapter 31: Flow Control: Branching with case

### Chapter 32: Positional Parameters

### Chapter 33: Flow Control: Looping with for

### Chapter 34: Strings and Numbers

### Chapter 35: Arrays

### Chapter 36: Exotica

Index