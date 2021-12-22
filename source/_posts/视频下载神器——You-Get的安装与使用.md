---
title: 视频下载神器——You-Get的安装与使用
date: 2021-06-27 01:43:57
abbrlink: 74f1c0a5
tags:
  - You-Get
  - Python
  - 工具
categories:
  - 工具分享
top_img: 'https://cdn.jsdelivr.net/gh/b1acksoil/bsblog-assets/img/article/74f1c0a5/top_img.png'
cover: 'https://cdn.jsdelivr.net/gh/b1acksoil/bsblog-assets/img/article/74f1c0a5/top_img.png'
---

看视频正看得兴起的时候突然缓冲半天？想要在没有网的环境下观看，却发现没有会员不能下载？为解决这种层出不穷的麻烦事，在此介绍一款开源的视频下载神器——[You-Get](https://github.com/soimort/you-get)。

# 介绍
[You-Get](https://github.com/soimort/you-get) 是一款由 [soimort](https://github.com/soimort) 使用Python开发的开源**命令行**视频/图片/音频下载器。截止本文写作日期，You-Get已支持78家网站的资源下载，而且支持版权视频下载（这**并不**意味着可以无会员白嫖会员资源，后面会讲）

{% hideToggle 网站支持列表 %}

| 网站 | URL | 视频 | 图片 | 音频 |
| :--: | :-- | :-----: | :-----: | :-----: |
| **163<br/>网易视频<br/>网易云音乐** | <http://v.163.com/><br/><http://music.163.com/> |✓| |✓|
| 56网     | <http://www.56.com/>           |✓| | |
| **AcFun** | <http://www.acfun.cn/>        |✓| | |
| **Baidu<br/>百度贴吧** | <http://tieba.baidu.com/> |✓|✓| |
| 爆米花网 | <http://www.baomihua.com/>     |✓| | |
| **bilibili<br/>哔哩哔哩** | <http://www.bilibili.com/> |✓|✓|✓|
| 豆瓣     | <http://www.douban.com/>       |✓| |✓|
| 斗鱼     | <http://www.douyutv.com/>      |✓| | |
| 凤凰视频 | <http://v.ifeng.com/>          |✓| | |
| 风行网   | <http://www.fun.tv/>           |✓| | |
| iQIYI<br/>爱奇艺 | <http://www.iqiyi.com/> |✓| | |
| 激动网   | <http://www.joy.cn/>           |✓| | |
| 酷6网    | <http://www.ku6.com/>          |✓| | |
| 酷狗音乐 | <http://www.kugou.com/>        | | |✓|
| 酷我音乐 | <http://www.kuwo.cn/>          | | |✓|
| 乐视网   | <http://www.le.com/>           |✓| | |
| 荔枝FM   | <http://www.lizhi.fm/>         | | |✓|
| 懒人听书 | <http://www.lrts.me/>          | | |✓|
| 秒拍     | <http://www.miaopai.com/>      |✓| | |
| MioMio弹幕网 | <http://www.miomio.tv/>    |✓| | |
| MissEvan<br/>猫耳FM | <http://www.missevan.com/> | | |✓|
| 痞客邦   | <https://www.pixnet.net/>      |✓| | |
| PPTV聚力 | <http://www.pptv.com/>         |✓| | |
| 齐鲁网   | <http://v.iqilu.com/>          |✓| | |
| QQ<br/>腾讯视频 | <http://v.qq.com/>      |✓| | |
| 企鹅直播 | <http://live.qq.com/>          |✓| | |
| Sina<br/>新浪视频<br/>微博秒拍视频 | <http://video.sina.com.cn/><br/><http://video.weibo.com/> |✓| | |
| Sohu<br/>搜狐视频 | <http://tv.sohu.com/> |✓| | |
| **Tudou<br/>土豆** | <http://www.tudou.com/> |✓| | |
| 阳光卫视 | <http://www.isuntv.com/>       |✓| | |
| **Youku<br/>优酷** | <http://www.youku.com/> |✓| | |
| 战旗TV   | <http://www.zhanqi.tv/lives>   |✓| | |
| 央视网   | <http://www.cntv.cn/>          |✓| | |
| Naver<br/>네이버 | <http://tvcast.naver.com/>     |✓| | |
| 芒果TV   | <http://www.mgtv.com/>         |✓| | |
| 火猫TV   | <http://www.huomao.com/>       |✓| | |
| 阳光宽频网 | <http://www.365yg.com/>      |✓| | |
| 西瓜视频 | <https://www.ixigua.com/>      |✓| | |
| 新片场 | <https://www.xinpianchang.com/>      |✓| | |
| 快手 | <https://www.kuaishou.com/>      |✓|✓| |
| 抖音 | <https://www.douyin.com/>      |✓| | |
| TikTok | <https://www.tiktok.com/>      |✓| | |
| 中国体育(TV) | <http://v.zhibo.tv/> </br><http://video.zhibo.tv/>    |✓| | |
| 知乎 | <https://www.zhihu.com/>      |✓| | |
| **YouTube** | <https://www.youtube.com/>    |✓| | |
| **Twitter** | <https://twitter.com/>        |✓|✓| |
| VK          | <http://vk.com/>              |✓|✓| |
| Vine        | <https://vine.co/>            |✓| | |
| Vimeo       | <https://vimeo.com/>          |✓| | |
| Veoh        | <http://www.veoh.com/>        |✓| | |
| **Tumblr**  | <https://www.tumblr.com/>     |✓|✓|✓|
| TED         | <http://www.ted.com/>         |✓| | |
| SoundCloud  | <https://soundcloud.com/>     | | |✓|
| SHOWROOM    | <https://www.showroom-live.com/> |✓| | |
| Pinterest   | <https://www.pinterest.com/>  | |✓| |
| MTV81       | <http://www.mtv81.com/>       |✓| | |
| Mixcloud    | <https://www.mixcloud.com/>   | | |✓|
| Metacafe    | <http://www.metacafe.com/>    |✓| | |
| Magisto     | <http://www.magisto.com/>     |✓| | |
| Khan Academy | <https://www.khanacademy.org/> |✓| | |
| Internet Archive | <https://archive.org/>   |✓| | |
| **Instagram** | <https://instagram.com/>    |✓|✓| |
| InfoQ       | <http://www.infoq.com/presentations/> |✓| | |
| Imgur       | <http://imgur.com/>           | |✓| |
| Heavy Music Archive | <http://www.heavy-music.ru/> | | |✓|
| Freesound   | <http://www.freesound.org/>   | | |✓|
| Flickr      | <https://www.flickr.com/>     |✓|✓| |
| FC2 Video   | <http://video.fc2.com/>       |✓| | |
| Facebook    | <https://www.facebook.com/>   |✓| | |
| eHow        | <http://www.ehow.com/>        |✓| | |
| Dailymotion | <http://www.dailymotion.com/> |✓| | |
| Coub        | <http://coub.com/>            |✓| | |
| CBS         | <http://www.cbs.com/>         |✓| | |
| Bandcamp    | <http://bandcamp.com/>        | | |✓|
| AliveThai   | <http://alive.in.th/>         |✓| | |
| interest.me | <http://ch.interest.me/tvn>   |✓| | |
| **755<br/>ナナゴーゴー** | <http://7gogo.jp/> |✓|✓| |
| **niconico<br/>ニコニコ動画** | <http://www.nicovideo.jp/> |✓| | |

{% endhideToggle %}

# 安装
## 环境需求
安装You-Get需要以下运行环境
- [Python](https://www.python.org/downloads/) 3.2 或更高
- [FFMpeg](https://www.ffmpeg.org/) 1.0 或更高
- (可选) [RTMPDump](https://rtmpdump.mplayerhq.hu/)

## 安装
选择一种安装方式即可
### 通过pip安装
```bash
$ pip3 install you-get
```
{% note info %}
Windows系统可能会提示找不到命令，此时可以用`pip`代替`pip3`
{% endnote %}

### 从GitHub下载安装
从GitHub下载[稳定版\(stable\)](https://github.com/soimort/you-get/archive/master.zip)或[开发版\(develop\)](https://github.com/soimort/you-get/archive/develop.zip)（更多的热更新和不稳定特性）。解压并将包含有`you-get`可执行文件加入系统环境目录(PATH)，找到解压目录中的`setup.py`，并执行
```bash
$ sudo python3 setup.py install    # 全局安装
```
或者
```bash
$ python3 setup.py install --user    # 针对当前用户安装
```
{% note info %}
Windows系统可能需要将`python3`替换为`python`，并将`sudo`移除
{% endnote %}

### Git Clone
克隆you-get仓库
```bash
$ git clone git://github.com/soimort/you-get.git
```

### Homebrew (Mac Only)
使用`Homebrew`安装（若未安装Homebrew可以参考这篇文章：[Mac必备神器Homebrew](https://zhuanlan.zhihu.com/p/59805070)）
```bash
$ brew install you-get
```

## 更新
如果你通过`pip`安装，那么你可以执行以下命令来更新`you-get`：
```bash
$ pip3 install --upgrade you-get
```
如果你通过其他方式安装，你可以执行以下命令：
```bash
$ you-get https://github.com/soimort/you-get/archive/master.zip
```
如果你使用开发版，你可以这样更新：
```bash
$ pip3 install --upgrade git+https://github.com/soimort/you-get@develop
```

# 使用
如果你想下载一个视频，你得先复制它的链接，然后看看有哪些清晰度和格式可选。以b站举例：
```output
$ you-get -i https://b23.tv/ep84363

site:                Bilibili
title:               某科学的超电磁炮：第24话 亲爱的朋友
streams:             # Available quality and codecs
    [ DASH ] ____________________________________
    - format:        dash-flv
      container:     mp4
      quality:       高清 1080P
      size:          225.1 MiB (236051580 bytes)
    # download-with: you-get --format=dash-flv [URL]

    - format:        dash-flv720
      container:     mp4
      quality:       高清 720P
      size:          178.0 MiB (186614140 bytes)
    # download-with: you-get --format=dash-flv720 [URL]

    - format:        dash-flv480
      container:     mp4
      quality:       清晰 480P
      size:          106.1 MiB (111270053 bytes)
    # download-with: you-get --format=dash-flv480 [URL]

    - format:        dash-flv360
      container:     mp4
      quality:       流畅 360P
      size:          75.8 MiB (79492115 bytes)
    # download-with: you-get --format=dash-flv360 [URL]

    [ DEFAULT ] _________________________________
    - format:        flv
      container:     flv
      quality:       高清 1080P
      size:          351.8 MiB (368884547 bytes)
    # download-with: you-get --format=flv [URL]

    - format:        flv720
      container:     flv
      quality:       高清 720P
      size:          273.0 MiB (286301511 bytes)
    # download-with: you-get --format=flv720 [URL]

    - format:        flv360
      container:     flv
      quality:       流畅 360P
      size:          76.2 MiB (79917137 bytes)
    # download-with: you-get --format=flv360 [URL]
```
决定好了想要下载哪种格式和清晰度，执行以下命令来下载：
```output
$ you-get --format=dash-flv360 https://b23.tv/ep84363
site:                Bilibili
title:               某科学的超电磁炮：第24话 亲爱的朋友
stream:
    - format:        dash-flv360
      container:     mp4
      quality:       流畅 360P
      size:          75.8 MiB (79492115 bytes)
    # download-with: you-get --format=dash-flv360 [URL]

Downloading 某科学的超电磁炮：第24话 亲爱的朋友.mp4 ...
 100% ( 75.8/ 75.8MB) ├████████████████████████████████████████┤[2/2]  2 MB/s
Merging video parts... Merged into 某科学的超电磁炮：第24话 亲爱的朋友.mp4

Downloading 某科学的超电磁炮：第24话 亲爱的朋友.cmt.xml ...
```
> 上面例子中同时下载的`xml`文件是b站的弹幕文件。
> `--format=dash-flv360`选项也可简写为`-F dash-flv360`

{% note info %}
如果你发现下载完视频没有合并（典型例子是当前目录下出现了两段断开的视频，名字分别为`视频名[00].mp4`和`视频名[01].mp4`），则可能是因为你没有正确安装FFMpeg。
各Linux发行版可以使用各自的包管理器安装，如Debian/Ubuntu使用`sudo apt install ffmpeg`
Mac： 使用Homebrew `brew install ffmpeg`
Windows中FFMpeg的安装可以参照这篇博客：[FFmpeg使用教程（一）-windows安装配置ffmpeg](https://www.jianshu.com/p/2b609afb9800)
{% endnote %}

## 断点续传
在下载过程中，你可能不小心终止了下载（例如按了`Ctrl+C`或突然断网）。这时你会在当前目录找到后缀名为`.download`的文件。这是`you-get`下载的缓存文件，下一次重新执行下载命令时，`you-get`会自动从上次的断点重新开始下载，而不用担心需要重新下载。
不想要断点续传时，可以直接删除`.download`文件。

## 下载版权资源
有一些视频是无法直接下载的，例如各大网站的会员电影、电视剧，b站的大会员番剧等等。此时需要用到`you-get`的另外一项功能：加载cookies。
> cookies （从客户端的硬盘读取数据的一种技术）
> cookies中文名称为小型文本文件，是某些网站为了辨别用户身份，进行Session跟踪而储存在用户本地终端上的数据（通常经过加密），由用户客户端计算机暂时或永久保存的信息。
> 摘自 [百度百科](https://baike.baidu.com/item/Cookies/187064)

目前`you-get`支持两种格式的cookies：Mozilla Firefox(火狐浏览器)`cookies.sqlite` 和 Netscape `cookies.txt`

{% note info %}
Google Chrome/Chromium 浏览器有插件（例如[EditThisCookie](https://chrome.google.com/webstore/detail/editthiscookie/fngmhnnpilhplaeedifhccceomclgfbg/related?utm_source=chrome-ntp-icon&pli=1)）可以将cookies文件转换成you-get可以识别的格式（如Netscape `cookies.txt`）
{% endnote %}

首先在以上浏览器中打开需要下载的网站，并登录会员帐号
登录完成后找到cookies文件：
Windows：`C:\Users\<你的用户名>\AppData\Roaming\Mozilla\Firefox\Profiles\cookies.sqlite`
Linux/Mac：`~/.mozilla/firefox/一些随机的字母.default-release/cookies.sqlite`

将其**复制**到一个方便的位置，以便稍后引用

{% note warning %}
不要直接移动（或剪切） cookies 文件！这会导致你的浏览器出现异常（通常表现为网站需要重新登录并清除数据），所以复制就好
{% endnote %}

打开命令行，使用`-c`选项引用cookies文件下载：
```bash
$ you-get -c cookies文件位置 -F 格式 [会员视频URL链接]
```
例如：
```bash
$ you-get -c ~/cookies.sqlite -F dash-flv https://b23.tv/ep248715
```
即可下载会员资源。