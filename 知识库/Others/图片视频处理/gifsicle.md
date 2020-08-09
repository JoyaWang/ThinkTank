

## gifsicle



想要达到这样的压缩优化效果，我推荐使用一款命令行工具 gifsicle，建议通过 homebrew 来安装它。

- 如果你的电脑里还没有 homebrew，就打开 Terminal，输入这串命令安装 homebrew：

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

- 一长串字符闪过之后，接着输入命令安装 gifsicle：

```
brew install gifsicle
```

- 使用 gifsicle 压缩 GIF 时，用这个命令：

```
gifsicle -O3 [想要压缩的图片] -o [新图片名]
```

其实 gifsicle 也有着较为丰富可调节参数，但是最实用的还是用 `-O3` 让它自动为你选择压缩方案，一般能在画质和体积之间取得平衡，并且第一帧之后的每一帧都能得到优化。

```shell
gifsicle --colors 256 -o3 b.gif -o a1.gif 
```

