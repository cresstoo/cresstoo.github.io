title: 用FFmpeg和ImageMagick制作拼图
date: 2014-10-13 17:01:14
tags: ffmpeg
---
有个小mp4视频想要做全屏自动循环播放，部分手机浏览器并不支持，转成gif画质损失文件庞大，于是要转成分片的拼图，最终控制CSS来实现动画播放。

<!-- more -->

### 所需工具：ffmpeg、ImageMagick。

1.  原始视频为1920×1080，需要裁切为640×1136(IP5)的竖幅，只能先按比例裁减为608×1080 

    `ffmpeg -i sequence.mp4 -filter:v "crop=640:1139:100:100" -crf 18 sequence01.mp4`

    2.用ffmpeg设置每秒抓2帧，尺寸为640×1136，自动命名，最终截图17张（最好不要太多）

    `ffmpeg -i sequence01.mp4 -r 2 -f image2 -s 640x1136 s01_%03d.jpg`

    3.用imagemagick对原始截图进行压缩，在Stackoverflow 学到一招用点高斯模糊

    `mogrify -strip -interlace Plane -gaussian-blur 0.05 -quality 75% *.jpg`

    4.最后对所有图片进行垂直拼图(-是垂直，+是横向)

    `convert -append *.jpg filmstrip01.jpg`

### 处理前后 大小

原始视频 2.5mb
原始截图 3.44mb
优化之后 384kb
最终拼图 367kb

最后再写一个脚本就完美了……（bash手册丢一边……