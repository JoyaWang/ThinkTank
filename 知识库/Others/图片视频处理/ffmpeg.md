

## ffmpeg

压缩视频并转换格式

ffmpeg -i `路径/PM.mov` -b:v 2048k -s 1920x1080 `路径/video.mp4`

转换格式【超快速度】

ffmpeg -i `路径/video.m4v` -c:v libx264 -preset ultrafast `test.mp4`

