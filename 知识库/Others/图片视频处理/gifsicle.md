

## Gif

## Gif Brewery 3

在官方教程中，开发者建议用户将 frame delay 设置为 42 ms，什么意思呢？根据公式计算，FPS(frames per second) = (1000) / (frame delay），也就是当你选择 42ms 时，FPS 为 24，如果设置为更高的 100ms，FPS 为 10。

假设你要制作一个长度为 10 秒的动图，frame delay 为 42ms，那么需要的帧数（frame count）就是：10s x 24fps = 240 帧，这样能带来更细腻的画面效果。反过来，如果你关心文件大小，建议更高的 frame delay，也就是 100ms，相当于每秒显示10帧，可以制作更小的 GIF，如果你想要更流畅的播放效果，选择 40ms-50ms 的 frame delay 即可。

总之，颜色数量、图像尺寸和帧数的适当调整才能保证文件的可传播性，根据需求设置即可。

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



-O1 Stores only the changed portion of each image. This is the default.
 -O2 Also uses transparency to shrink the file further.
 -O3 Try several optimization methods (usually slower, sometimes better results).
 Gifsicle是用于创建，编辑和获取有关GIF图像和动画的信息的命令行工具。使用gifsicle制作GIF动画很容易



