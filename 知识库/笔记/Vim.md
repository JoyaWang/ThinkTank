# Vim

- 打开文件

  > sudo vim httpd-dav.conf 打开要编辑的文件

- 搜索

  > 别管光标位置，直接输入命令行:/httpd-dav.conf （因为现在并非编辑状态，"/"代表搜索的意思），然后回车，光标自动跳到那个位置

- 将光标移动到行首(快捷键0)

- 修改并保存：

  > 输入i，变成编辑状态
  >
  > 输入完毕后，按esc退出编辑状态
  >
  > :wq保存退出
  >
  > :qa 不保存并退出





## pacvim 游戏

pacvim [LEVEL_NUMBER] [MODE]

上述代码中的 LEVELNumber 取值范围为 0 - 9，数字越大，难度越高。

Mode 可选 N 或 H，N 表示 Normal ，正常难度；H 则表示 Hard ，困难。

pacvim 8 n