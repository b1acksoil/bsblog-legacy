---
title: FFmpeg的基本使用
abbrlink: 972a1a27
tags:
  - FFmpeg
  - 工具
categories:
  - 工具分享
top_img: 'https://cdn.jsdelivr.net/gh/b1acksoil/blog-cdn/img/article/972a1a27/top_img.png'
cover: 'https://cdn.jsdelivr.net/gh/b1acksoil/blog-cdn/img/article/972a1a27/top_img.png'
date: 2021-08-25 01:10:38
---

> FFmpeg是一套可以用来记录、转换数字音频、视频，并能将其转化为流的开源计算机程序。采用LGPL或GPL许可证。它提供了录制、转换以及流化音视频的完整解决方案。它包含了非常先进的音频/视频编解码库libavcodec，为了保证高可移植性和编解码质量，libavcodec里很多code都是从头开发的。
> 
> ——百度百科

简单来说，FFmpeg 是一套集视频/音频的格式转换、合成、裁切等等实用功能于一体的开源工具。截止本文写作日期，FFmpeg 已支持 **365** 种不同的视频/音频格式。FFmpeg 发展十余年，在世界上的应用十分广泛，例如有时我们用到的优酷，爱奇艺等播放器软件，内部都集成了 FFmpeg （虽然一些是修改过的）。FFmpeg 内置了领先的音视频编码库，可以有效利用多线程和GPU加速，为用户在诸多使用场景下提供了优秀的体验。

[FFmpeg 官网](http://ffmpeg.org/)

# 安装
## Windows
{% note info %}
此为官方网站上给出的 Windows Build 渠道，请放心下载
{% endnote %}

前往 [FFmpeg Windows Builds](https://www.gyan.dev/ffmpeg/builds/)，往下翻找到 `release` 一栏，点击第一个链接下载（ffmpeg-release-full.7z）

![Release Full Build](https://cdn.jsdelivr.net/gh/b1acksoil/blog-cdn/img/article/972a1a27/download_windows.png)

使用 [7-Zip](https://www.7-zip.org/) 等支持 `7z` 格式的解压软件解压即可

## Linux
### Debain/Ubuntu 系
执行以下命令安装：
```bash
$ sudo apt install ffmpeg
```

### Termux
```bash
$ pkg install ffmpeg
```

### 其他系的 Linux 发行版
待更新...

## macOS
{% note info %}
此为官方网站上给出的 macOS Build 渠道，请放心下载
{% endnote %}

前往 [Static builds for macOS 64-bit](https://evermeet.cx/ffmpeg/) ，点击 FFmpeg 一栏的第一个下载按钮下载 7z 压缩包

# 使用
{% note warning %}
Windows 和 macOS 由于不是使用包管理器安装，需要使用 `ffmpeg` 可执行文件的绝对路径来代替下文的 `ffmpeg` 命令。常见的做法是将可执行文件拖入命令窗口来自动填入绝对路径。  
除了使用这种办法，也可以使用添加环境变量的方式，具体请自行百度。
{% endnote %}

检查 FFmpeg 是否正确安装：
```bash
$ ffmpeg -version
```

如果输出了一些参数、库版本等信息，则成功安装。

{% note info %}
**Tips:**
- 可以在目录中迅速定位想要的内容。
- 如果想要了解具体参数的含义，可以查阅 `附录：参数解析`
- 如果遇到报错等问题，可以在下一节 `问题解决` 中寻找对应的答案。如果问题没有收录，可以查阅百度/谷歌等，或者在评论区反馈（不一定能成功解决）。
{% endnote %}

## 格式转换

{% note info %}
**Tips:** 可以使用 `ffmpeg -formats` 命令来查看所有支持的格式。
{% endnote %}

{% note warning %}
检索后可以发现，某些格式例如网易云音乐会员下载的 `ncm` 格式是不被 FFmpeg 所支持的。严格来说它们并不是音频格式，内部包含了加密保护。对于这种格式的解密/转换，请自行寻找专用软件，如 ncmdump 等。
{% endnote %}
### 同为音频或视频，互转格式
> 情景：我们下载了一个 `mp3` 格式的音乐，名为 `music.mp3` ，我们想要把它转换为 `wav` 格式，名为 `new_music.wav`

首先前往该文件的目录下，使用以下命令即可，FFmpeg 会自动判断文件格式并完成转换：
```bash
$ ffmpeg -i music.mp3 new_music.wav
```

命令解析：
```
$ ffmpeg -i 输入文件 输出文件
```

### 单独提取音/视频
> 情景：我们有一个名为 `ocean_cat.mp4` 的视频，想要把它的音频提取出来，保存在 `damedane.mp3` 里

使用以下命令，FFmpeg 会自动转码至指定格式：
```bash
$ ffmpeg -i ocean_cat.mp4 -vn damedane.mp3

# 或者将视频单独提取到 damedane.mp4
$ ffmpeg -i ocean_cat.mp4 -an damedane.mp4
```

命令解析：
```bash
$ ffmpeg -i 输入文件 -vn 输出文件   # 提取音频
$ ffmpeg -i 输入文件 -an 输出文件   # 提取视频
```

## 音视频裁剪
> 情景：我们有一个 `mp3` 格式的音乐，名为 `mopemope.mp3` ，全长1分52秒。我们想要截取其中0分45秒到1分38秒共53秒的内容，并保存为 `good_children.flac`。

注：视频转换同理。FFmpeg 会自动判断文件扩展名并转换格式。

方式一：指定起始时间和终点时间
```bash
$ ffmpeg -i mopemope.mp3 -ss 00:00:45.0 -to 00:01:38.0 good_children.flac
```

命令解析：
```bash
$ ffmpeg -i 输入文件 -ss 起始时间 -to 终点时间 输出文件
```

方式二：指定起始时间和持续时间
```bash
$ ffmpeg -i mopemope.mp3 -ss 00:00:45.0 -t 00:00:53.0 good_children.flac
```

命令解析：
```bash
$ ffmpeg -i 输入文件 -ss 起始时间 -t 持续时间 输出文件
```

{% note info %}
**Tips:** 时间也可以简写成 `时:分:秒` ，或是直接写秒数。使用负号可以指定从末尾开始算起的时间，如 `-to -00:00:10` 意为设置终点时间为该音/视频结束前的第十秒。
{% endnote %}

## 音视频处理
### 码率调整
关于码率详见 [比特率 - 百度百科](https://baike.baidu.com/item/%E6%AF%94%E7%89%B9%E7%8E%87/1022775)、[视频码率 - 百度百科](https://baike.baidu.com/item/%E8%A7%86%E9%A2%91%E7%A0%81%E7%8E%87/10008023)

一个音/视频的体积太大太占空间，我们就可以降低码率来把它压缩（对于视频还可以选择降低分辨率的方式）。视频码率较低会导致变化较快的画面出现失真、模糊、色块等现象；音频的码率直接关系到音质的好坏。但降低码率可以有效压缩体积，提高传输效率。

例如要将一个平均码率为 8Mbps 的视频 `aaa.mp4` 降到 2Mbps，可以这样（音频同样适用）：
```bash
$ ffmpeg -i aaa.mp4 -b 2m aaa.mp4
```
如果要分开处理一个视频的视频部分和音频部分，可以使用 `-b:v` 和 `-b:a` 参数：
```bash
$ ffmpeg -i aaa.mp4 -b:v 2m -b:a 240k aaa.mp4
```

命令解析：
```bash
$ ffmpeg -i 输入文件 -b 指定码率 输出文件
$ ffmpeg -i 输入视频文件 -b:v 指定视频码率 -b:a 指定音频码率 输出文件
```

### 视频分辨率调整
我们也可以使用降低分辨率的方式来压缩视频体积。`-vf scale`（缩放）过滤器提供了这一功能。

例如将一个 1080P (1920x1080) 的视频降到 720P (1280x720) ，可以这样做：
```bash
$ ffmpeg -i aaa.mp4 -vf scale=1280:720 aaa.mp4
```

命令解析：
```bash
$ ffmpeg -i 输入文件 -vf scale=输出宽度:输出高度 输出文件
```

{% note info %}
**Tips:** 输入分辨率时，可以将宽度或高度其中一个写为 `-1` ，例如 `1280:-1` ，FFmpeg会自动按照原始比例计算相对应的宽/高。
{% endnote %}

### 转换视频帧为图片
> 情景：有一个视频 `aaa.mp4` ，要以5秒1张的速度将它转换成图片，并保存到 `output_img` 文件夹里

可以搭配 `-vf fps` 过滤器来完成这一功能：
```bash
$ mkdir output_img
$ ffmpeg -i aaa.mp4 -vf fps=1/5 -qscale 0 -f image2 output_img/img-%3d.jpg
```

注意输出文件名里的 `%3d` 。这指定了图片的文件名格式，里面的数字代表编号的补位长度。例如输出文件名设置为 `img-%3d.jpg` ，输出的文件就是 `img-001.jpg` `img-002.jpg` `img-003.jpg`......如果设置为 `img-%4d.jpg` ，输出文件就是 `img-0001.jpg` `img-0002.jpg` `img-0003.jpg`......

命令解析：
```bash
$ ffmpeg -i 输入文件 -vf fps=1/每帧秒数 -qscale 0 -f image2 输出文件（包含文件名格式）
# 或者
$ ffmpeg -i 输入文件 -vf fps=每秒帧数 -qscale 0 -f image2 输出文件（包含文件名格式）
```

# 问题解决
## Too many packets buffered...
> 报错：  
> Too many packets buffered for output stream xxx.  
> xxx frames left in the queue on closing

有些视频数据有问题，导致视频处理过快，容器封装时队列溢出。  
可以通过增大容器封装队列大小解决，比如设置最大为1024：  
在**输入文件后方**添加 `-max_muxing_queue_size 1024` ，例如：
```bash
$ ffmpeg -i video.mp4 -max_muxing_queue_size 1024 output.avi
```
参考&致谢： [解决FFmpeg抛出的“Too many packets buffered for output stream 0:1.”异常](https://blog.csdn.net/COCO56/article/details/109321651)

# 附录：参数解析
## 参数
表格按字母顺序排列，仅列出上文提到的。

|      参数      |            含义             |
|---------------|-----------------------------|
| `-an`         | 不处理音频                   |
| `-b 比特率`    | 改变一个音/视频的比特率（码率）  |
| `-b:a 比特率`  | 单独改变音频的比特率（码率）    |
| `-b:v 比特率`  | 单独改变视频的比特率（码率）    |
| `-f 格式`      | 强制指定输出格式              |
| `-formats`    | 查看 FFmpeg 支持的格式列表     |
| `-i 输入文件`  | 指定输入文件，后跟输入文件的路径 |
| `-max_muxing_queue_size 大小` | 改变最大容器封装队列大小，需要写在输入文件的后面 |
| `-qscale 质量` | 控制动态比特率（VBR）质量，值越小越好。设置为 `0` 则保留原始质量 |
| `-ss 起始时间` | 指定起始时间，格式为 `时:分:秒.毫秒` |
| `-t 持续时间`  | 指定持续时间，格式为 `时:分:秒.毫秒` |
| `-to 终点时间` | 指定终点时间，格式为 `时:分:秒.毫秒` |
| `-vf 过滤器选项`| 指定视频的过滤器选项。         |
| `-vn`         | 不处理视频                   |
