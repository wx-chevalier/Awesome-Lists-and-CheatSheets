> 本文节选自 [Live CheatSheet | 直播技术理论基础与实践概论](https://github.com/wx-chevalier/Awesome-CheatSheets/blob/master/IndustrialApplication/IM/Live-CheatSheet.md)，**很多内容非作者原创**，而是对 [Live Links](https://github.com/wx-chevalier/Awesome-Lists/blob/master/IndustrialApplication/IM/Live-List.md) 中列举出的多篇文章的盘点总结，更多直播相关内容可以前往 [NGTE Website](https://ng-tech.icu/books/home/#/search?query=%E7%9B%B4%E6%92%AD) 交互式检索或 [MushiChat](https://github.com/wx-chevalier/MushiChat) 查看代码。

# Live CheatSheet | 直播技术理论基础与实践概论

音视频直播的基本流程都是`采集 → 编码推流 → 网络分发 → 解码 → 播放`这五大环节，其中又会涉及平台硬件、编解码、网络传输、服务并发、数字信号处理、在线学习等多方面技术。从交互模式上，又可以泛分为单对单模式与会议模式两大类；从实时性要求上，直播又可以分为伪实时、准实时与真实时三个等级:

- 伪实时：视频消费延迟超过 3 秒，单向观看实时，通用架构是 CDN + RTMP + HLS，譬如很多的直播平台

- 准实时：视频消费延迟 1 ~ 3 秒，能进行双方互动但互动有障碍；可以通过 TCP/UDP + FLV 已经实现了这类技术，譬如 YY 直播等

- 真实时：视频消费延迟 < 1 秒，平均 500 毫秒，譬如 QQ、微信、Skype 和 WebRTC 等

# 编解码

视频封装格式就是我们通常所说的 .mp4,.flv,.ogv,.webm 等，它其实就是一个盒子，用来将实际的视频流以一定的顺序放入，确保播放的有序和完整性。视频压缩格式(视频编码)就是指能够对数字视频进行压缩或者解压缩(视频解码)的程序或者设备。通常这种压缩属于有损数据压缩。

视频压缩格式和视频格式具体的区别就是，它是将原始的视频码流变为可用的数字编码。首先，由原始数码设备提供相关的数字信号流，然后经由视频压缩算法，大幅度的减少流的大小，然后交给视频盒子，打上相应的 dts，pts 字段，最终生成可用的视频文件。视频编码也可以指通过过特定的压缩技术，将某个视频格式转换成另一种视频格式。

![image](https://user-images.githubusercontent.com/5803001/47571461-2cbb4a80-d96b-11e8-855f-19dc0c8f8305.png)

## 视频封装格式

常见的视频封装格式(简称：视频格式)包括了 AVI，MPEG，VOB 等，即相当于一种储存视频信息的容器，由相应的公司开发出来的。

![image](https://user-images.githubusercontent.com/5803001/47571490-3e9ced80-d96b-11e8-97ec-f1fd8af219e2.png)

### AVI

AVI 格式(后缀为.AVI)：它的英文全称为 Audio Video Interleaved，即音频视频交错格式。它于 1992 年被 Microsoft 公司推出。

这种视频格式的优点是图像质量好。由于无损 AVI 可以保存 alpha 通道，经常被我们使用。缺点太多，体积过于庞大，而且更加糟糕的是压缩标准不统一，最普遍的现象就是高版本 Windows 媒体播放器播放不了采用早期编码编辑的 AVI 格式视频，而低版本 Windows 媒体播放器又播放不了采用最新编码编辑的 AVI 格式视频，所以我们在进行一些 AVI 格式的视频播放时常会出现由于视频编码问题而造成的视频不能播放或即使能够播放，但存在不能调节播放进度和播放时只有声音没有图像等一些莫名其妙的问题。

### DV-AVI

DV-AVI 格式(后缀为.AVI)：DV 的英文全称是 Digital Video Format，是由索尼、松下、JVC 等多家厂商联合提出的一种家用数字视频格式。

数字摄像机就是使用这种格式记录视频数据的。它可以通过电脑的 IEEE 1394 端口传输视频数据到电脑，也可以将电脑中编辑好的的视频数据回录到数码摄像机中。这种视频格式的文件扩展名也是 avi。电视台采用录像带记录模拟信号，通过 EDIUS 由 IEEE 1394 端口采集卡从录像带中采集出来的视频就是这种格式。

### MOV

QuickTime File Format 格式(后缀为.MOV)：美国 Apple 公司开发的一种视频格式，默认的播放器是苹果的 QuickTime。

具有较高的压缩比率和较完美的视频清晰度等特点，并可以保存 alpha 通道。大家可能注意到了，每次安装 EDIUS，我们都要安装苹果公司推出的 QuickTime。安装其目的就是为了支持 JPG 格式图像和 MOV 视频格式导入。

### MPEG

MPEG 格式(文件后缀可以是 .MPG .MPEG .MPE .DAT .VOB .ASF .3GP .MP4 等)：它的英文全称为 Moving Picture Experts Group，即运动图像专家组格式，该专家组建于 1988 年，专门负责为 CD 建立视频和音频标准，而成员都是为视频、音频及系统领域的技术专家。

MPEG 文件格式是运动图像压缩算法的国际标准。MPEG 格式目前有三个压缩标准，分别是 MPEG－1、MPEG－2、和 MPEG－4。MPEG－1、MPEG－2 目前已经使用较少，着重介绍 MPEG－4，其制定于 1998 年，MPEG－4 是为了播放流式媒体的高质量视频而专门设计的，以求使用最少的数据获得最佳的图像质量。目前 MPEG-4 最有吸引力的地方在于它能够保存接近于 DVD 画质的小体积视频文件。你可能一定注意到了，怎么没有 MPEG－3 编码，因为这个项目原本目标是为高分辨率电视(HDTV)设计，随后发现 MPEG-2 已足够 HDTV 应用，故 MPEG-3 的研发便中止。

### WMV

WMV 格式(后缀为.WMV .ASF)：它的英文全称为 Windows Media Video，也是微软推出的一种采用独立编码方式并且可以直接在网上实时观看视频节目的文件压缩格式。

WMV 格式的主要优点包括：本地或网络回放,丰富的流间关系以及扩展性等。WMV 格式需要在网站上播放，需要安装 Windows Media Player(简称 WMP)，很不方便，现在已经几乎没有网站采用了。

### Real Video

Real Video 格式(后缀为.RM .RMVB)：Real Networks 公司所制定的音频视频压缩规范称为 Real Media。

用户可以使用 RealPlayer 根据不同的网络传输速率制定出不同的压缩比率，从而实现在低速率的网络上进行影像数据实时传送和播放。RMVB 格式：这是一种由 RM 视频格式升级延伸出的新视频格式，当然性能上有很大的提升。RMVB 视频也是有着较明显的优势，一部大小为 700MB 左右的 DVD 影片，如果将其转录成同样品质的 RMVB 格式，其个头最多也就 400MB 左右。大家可能注意到了，以前在网络上下载电影和视频的时候，经常接触到 RMVB 格式，但是随着时代的发展这种格式被越来越多的更优秀的格式替代，著名的人人影视字幕组在 2013 年已经宣布不再压制 RMVB 格式视频。

### FLV

Flash Video 格式(后缀为.FLV)：由 Adobe Flash 延伸出来的的一种流行网络视频封装格式。随着视频网站的丰富，这个格式已经非常普及。

### MKV

Matroska 格式(后缀为.MKV)：是一种新的多媒体封装格式，这个封装格式可把多种不同编码的视频及 16 条或以上不同格式的音频和语言不同的字幕封装到一个 Matroska Media 档内。它也是其中一种开放源代码的多媒体封装格式。Matroska 同时还可以提供非常好的交互功能，而且比 MPEG 的方便、强大。

## 视频编解码

视频实际上就是一帧一帧的图片，拼接起来进行播放；标准的图像格式使用 RGB 三字节描述像素颜色值，会占用较大的存储空间与带宽。视频编解码器会根据前后图像的变化做运动检测，通过各种压缩把变化的结果发送到对方。

实时视频编码器需要考虑两个因素：编码计算量和码率带宽，实时视频会运行在移动端上，需要保证实时性就需要编码足够快，码率尽量小。基于这个原因现阶段一般认为 H.264 是最佳的实时视频编码器，而且各个移动平台也支持它的硬编码技术；譬如 1080P 进行过 H.264 编码后带宽也就在 200KB/S ~ 300KB/S 左右。

### 编码基础

总的来说，常用的编码方式分为三种：

- 变换编码：消除图像的帧内冗余。涉及到图像学里面的两个概念：空域和频域。空域就是我们物理的图片，频域就是将物理图片根据其颜色值等映射为数字大小。而变换编码的目的是利用频域实现去相关和能量集中。常用的正交变换有离散傅里叶变换，离散余弦变换等等。

- 运动估计和运动补偿：消除帧间冗余。视频压缩还存在时间上的关联性。例如，针对一些视频变化，背景图不变而只是图片中部分物体的移动，针对这种方式，可以只对相邻视频帧中变化的部分进行编码。

- 熵编码：提高压缩效率，熵编码主要是针对码节长度优化实现的。原理是针对信源中出现概率大的符号赋予短码，对于概率小的符号赋予长码，然后总的来说实现平均码长的最小值。编码方式（可变字长编码）有：霍夫曼编码、算术编码、游程编码等。

I,B,P 实际上是从运动补偿中引出来的，这里为了后面的方便先介绍一下。

- I 帧(I-frame): 学名叫做: `Intra-coded picture`。也可以叫做独立帧。该帧是编码器随机挑选的参考图像，换句话说，一个 I 帧本身就是一个静态图像。它是作为 B,P 帧的参考点。对于它的压缩，只能使用`熵` 和 `变化编码` 这两种方式进行帧内压缩。所以，它的运动学补偿基本没有。
- P 帧(P‑frame): 又叫做 `Predicted picture`--前向预测帧。即，他会根据前面一张图像，来进行图片间的动态压缩，它的压缩率和 I 帧比起来要高一些。
- B 帧(B‑frame): 又叫做 `Bi-predictive picture`-- 双向预测。它比 P 帧来说，还多了后一张图像的预测，所以它的压缩率更高。

![image](https://user-images.githubusercontent.com/5803001/47571758-ea463d80-d96b-11e8-93d3-dacdd68cbeec.png)

考虑到不同帧传输的无序性，我们还需要引入 PTS 与 DTS 来进行控制，使用 DTS 来解码，PTS 来进行播放。

- PTS(presentation time stamps): 显示时间戳，显示器从接受到解码到显示的时间。

- DTS(decoder timestamps): 解码时间戳。也表示该 sample 在整个流中的顺序

### H.26X

H.26X 系列由 ITU 国际电传视讯联盟主导包括，H.261、H.262、H.263、H.264、H.265 等：

1. H.261：主要在老的视频会议和视频电话产品中使用。

2. H.263：主要用在视频会议、视频电话和网络视频上。

3. H.264：H.264/MPEG-4 第十部分，或称 AVC(Advanced Video Coding，高级视频编码)，是一种视频压缩标准，一种被广泛使用的高精度视频的录制、压缩和发布格式。

4. H.265：高效率视频编码(High Efficiency Video Coding，简称 HEVC)是一种视频压缩标准，H.264/MPEG-4 AVC 的继任者。HEVC 被认为不仅提升图像质量，同时也能达到 H.264/MPEG-4 AVC 两倍之压缩率(等同于同样画面质量下比特率减少了 50%)，可支持 4K 分辨率甚至到超高画质电视，最高分辨率可达到 8192×4320(8K 分辨率)，这是目前发展的趋势。直至 2013 年，Potplayer 添加了对于 H.265 视频的解码，尚未有大众化编码软件出现。

H.264 是由 ITU 和 MPEG 两个组织共同提出的标准，整个编码器包括帧内预测编码、帧间预测编码、运动估计、熵编码等过程，支持分层编码技术(SVC)。单帧 720P 分辨率一般 PC 上的平均编码延迟 10 毫秒左右，码率范围 1200 ~ 2400kpbs，同等视频质量压缩率是 MPEG4 的 2 倍，H.264 也提供 VBR、ABR、CBR、CQ 等多种编码模式，各个移动平台兼容性好。

H.264 为了防止丢包和减小带宽还引入一种双向预测编码的 B 帧，B 帧以前面的 I 或 P 帧和后面的 P 帧为参考帧。H.264 为了防止中间 P 帧丢失视频图像会一直错误它引入分组序列（GOP）编码，也就是隔一段时间发一个全量 I 帧，上一个 I 帧与下一个 I 帧之间为一个分组 GOP。

![image](https://user-images.githubusercontent.com/5803001/47572890-a30d7c00-d96e-11e8-91d9-45a6bce68ad1.png)

在实时视频当中最好不要加入 B 帧，因为 B 帧是双向预测，需要根据后面的视频帧来编码，这会增大编解码延迟。

### MPGA 系列

MPEG 系列由 ISO 国际标准组织机构下属的 MPEG 运动图象专家组开发视频编码方面主要有：

1. MPEG-1 第二部分(MPEG-1 第二部分主要使用在 VCD 上，有些在线视频也使用这种格式。该编解码器的质量大致上和原有的 VHS 录像带相当。)

2. MPEG-2 第二部分(MPEG-2 第二部分等同于 H.262，使用在 DVD、SVCD 和大多数数字视频广播系统和有线分布系统(cable distribution systems)中。)

3. MPEG-4 第二部分(MPEG-4 第二部分标准可以使用在网络传输、广播和媒体存储上。比起 MPEG-2 和第一版的 H.263，它的压缩性能有所提高。)

4. MPEG-4 第十部分(MPEG-4 第十部分技术上和 ITU-T H.264 是相同的标准，有时候也被叫做“AVC”)最后这两个编码组织合作，诞生了 H.264/AVC 标准。ITU-T 给这个标准命名为 H.264，而 ISO/IEC 称它为 MPEG-4 高级视频编码(Advanced Video Coding，AVC)。

## 音频编码器

实时音视频除了视频编码器以外还需要音频编码器，音频编码器只需要考虑编码延迟和丢包容忍度，所以一般的 MP3、AAC、OGG 都不太适合作为实时音频编码器。从现在市场上来使用来看，Skype 研发的 Opus 已经成为实时音频主流的编码器。Opus 优点众多，编码计算量小、编码延迟 20ms、窄带编码-silk、宽带编码器 CELT、自带网络自适应编码等。

同视频编码类似，将原始的音频流按照一定的标准进行编码，上传，解码，同时在播放器里播放，当然音频也有许多编码标准，例如 PCM 编码，WMA 编码，AAC 编码等等。

# 直播协议

常用的直播协议包括了 HLS, RTMP 与 HTTP-FLV 这三种，其对比如下：

| 协议     | 优势                   | 缺陷                | 延迟性   |
| -------- | ---------------------- | ------------------- | -------- |
| HLS      | 支持性广               | 延时巨高            | 10s 以上 |
| RTMP     | 延时性好，灵活         | 量大的话，负载较高  | 1s 以上  |
| HTTP-FLV | 延时性好，游戏直播常用 | 只能在手机 APP 播放 | 2s 以上  |

## HLS

HLS, HTTP Live Streaming 是 Apple 提出的直播流协议，其将整个流分成一个个小的块，并基于 HTTP 的文件来下载；HLS 由两部分构成，一个是 .m3u8 文件，一个是 .ts 视频文件；每一个 .m3u8 文件，分别对应若干个 ts 文件，这些 ts 文件才是真正存放视频的数据，m3u8 文件只是存放了一些 ts 文件的配置信息和相关路径，当视频播放时，.m3u8 是动态改变的，video 标签会解析这个文件，并找到对应的 ts 文件来播放，所以一般为了加快速度，.m3u8 放在 web 服务器上，ts 文件放在 CDN 上。HLS 协议视频支持 H.264 格式的编码，支持的音频编码方式是 AAC 编码。

![image](https://user-images.githubusercontent.com/5803001/47569752-fbd91680-d966-11e8-8e5d-491fa49ec18e.png)

.m3u8 文件，其实就是以 UTF-8 编码的 m3u 文件，这个文件本身不能播放，只是存放了播放信息的文本文件：

```
#EXTM3U                 m3u文件头
#EXT-X-MEDIA-SEQUENCE   第一个TS分片的序列号
#EXT-X-TARGETDURATION   每个分片TS的最大的时长
#EXT-X-ALLOW-CACHE      是否允许cache
#EXT-X-ENDLIST          m3u8文件结束符
#EXTINF                 指定每个媒体段(ts)的持续时间（秒），仅对其后面的URI有效
mystream-12.ts
```

HLS 协议的使用也非常便捷，将 m3u8 直接写入到 src 中然后交与浏览器解析，也可以使用 fetch 来手动解析并且获取相关文件：

```js
<video controls autoplay>
  <source
    src="http://devimages.apple.com/iphone/samples/bipbop/masterplaylist.m3u8"
    type="application/vnd.apple.mpegurl"
  />
  <p class="warning">Your browser does not support HTML5 video.</p>
</video>
```

HLS 详细版的内容比上面的简版多了一个 playlist，也可以叫做 master。在 master 中，会根据网络段实现设置好不同的 m3u8 文件，比如，3G/4G/wifi 网速等。比如，一个 master 文件中为：

```
#EXTM3U
#EXT-X-VERSION:6
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=2855600,CODECS="avc1.4d001f,mp4a.40.2",RESOLUTION=960x540
live/medium.m3u8
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=5605600,CODECS="avc1.640028,mp4a.40.2",RESOLUTION=1280x720
live/high.m3u8
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=1755600,CODECS="avc1.42001f,mp4a.40.2",RESOLUTION=640x360
live/low.m3u8
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=545600,CODECS="avc1.42001e,mp4a.40.2",RESOLUTION=416x234
live/cellular.m3u8
```

以 high.m3u8 文件为例，其内容会包含：

```
#EXTM3U
#EXT-X-VERSION:6
#EXT-X-TARGETDURATION:10
#EXT-X-MEDIA-SEQUENCE:26
#EXTINF:9.901,
http://media.example.com/wifi/segment26.ts
#EXTINF:9.901,
http://media.example.com/wifi/segment27.ts
#EXTINF:9.501,
http://media.example.com/wifi/segment28.ts
```

该二级 m3u8 文件也可以称为 media 文件，其有三种类型：

- live playlist: 动态列表。顾名思义，该列表是动态变化的，里面的 ts 文件会实时更新，并且过期的 ts 索引会被删除。默认，情况下都是使用动态列表。
- event playlist: 静态列表。它和动态列表主要区别就是，原来的 ts 文件索引不会被删除，该列表是不断更新，而且文件大小会逐渐增大。它会在文件中，直接添加 #EXT-X-PLAYLIST-TYPE:EVENT 作为标识。
- VOD playlist: 全量列表。它就是将所有的 ts 文件都列在 list 当中。如果，使用该列表，就和播放一整个视频没有啥区别了。它是使用 #EXT-X-ENDLIST 表示文件结尾。

显而易见，HLS 的延时包含了 TCP 握手、m3u8 文件下载与解析、ts 文件下载与解析等多个步骤，可以缩短列表的长度和单个 ts 文件的大小来降低延迟，极致来说可以缩减列表长度为 1，并且 ts 的时长为 1s，但是这样会造成请求次数增加，增大服务器压力，当网速慢时回造成更多的缓冲，所以苹果官方推荐的 ts 时长时 10s，所以这样就会大改有 30s 的延迟。

## RTMP

RTMP，Real-Time Messaging Protocol 是由 Adobe 推出的音视频流传递协议；它通过一种自定义的协议，来完成对指定直播流的播放和相关的操作。在 Web 上可以通过 MSE（MediaSource Extensions）来接入 RTMP，基本思路是根据 WebSocket 直接建立长连接进行数据的交流和监听。RTMP 协议根据不同的套层，也可以分为：

- 纯 RTMP: 直接通过 TCP 连接，端口为 1935

- RTMPS: RTMP + TLS/SSL，用于安全性的交流。

- RTMPE: RTMP + encryption。在 RTMP 原始协议上使用，Adobe 自身的加密方法

- RTMPT: RTMP + HTTP。使用 HTTP 的方式来包裹 RTMP 流，这样能直接通过防火墙。不过，延迟性比较大。

- RTMFP: RMPT + UDP。该协议常常用于 P2P 的场景中，针对延时有变态的要求。

RTMP 内部是借由 TCP 长连接协议传输相关数据，所以，它的延时性非常低。并且，该协议灵活性非常好（所以，也很复杂），它可以根据 message stream ID 传输数据，也可以根据 chunk stream ID 传递数据。两者都可以起到流的划分作用。流的内容也主要分为：视频，音频，相关协议包等。

![image](https://user-images.githubusercontent.com/5803001/47570269-56bf3d80-d968-11e8-8e9c-4fc8a5e1a873.png)

## HTTP-FLV

RTMP 是直接将流的传输架在 RTMP 协议之上，而 HTTP-FLV 是在 RTMP 和客户端之间套了一层转码的过程，即：

![image](https://user-images.githubusercontent.com/5803001/47570314-735b7580-d968-11e8-9b7e-7c42d830afc9.png)

每个 FLV 文件是通过 HTTP 的方式获取的，所以，它通过抓包得出的协议头需要使用 chunked 编码：

```
Content-Type:video/x-flv
Expires:Fri, 10 Feb 2017 05:24:03 GMT
Pragma:no-cache
Transfer-Encoding:chunked
```

# 网络传输

单对单模式主要是怎么通过路由路径优化手段达到两点之间最优，这方面 SKYPE 首先提出基于 P2P 的 Real-time Network 模型。而 单对多模式是一个分发树模型，各个客户端节点需要就近接入离自己最近的服务器，然后在服务器与服务器构建一个实时通信网络。

## 基础

### 推流

所谓推流，就是将我们已经编码好的音视频数据发往视频流服务器中。实时音视频系统都是一个客户端到其他一个或者多个客户端的通信行为，这就意味着需要将客户端编码后的音视频数据传输到其他实时音视频系统都是一个客户端到其他一个或者多个客户端的通信行为，这就意味着需要将客户端编码后的音视频数据传输到其他客户端上，一般做法是先将数据实时上传到服务器上，服务器再进行转发到其他客户端，客户端这个上传音视频数据行为称为推流。

我们可以通过 Nginx 的 RTMP 扩展方便地搭建推流服务器：

```
rtmp {

    server {

        listen 1935;  #监听的端口

        chunk_size 4000;


        application hls {  #rtmp推流请求路径
            live on;
            hls on;
            hls_path /usr/local/var/www/hls;
            hls_fragment 5s;
        }
    }
}
```

推流会受到客户端网络的影响，例如：wifi 信号衰减、4G 弱网、拥挤的宽带网络等。为了应对这个问题，实时音视频系统会设计一个基于拥塞控制和 QOS 策略的推流模块。

### WebRTC

WebRTC 是一个开源项目，旨在使得浏览器能为实时通信（RTC）提供简单的 JavaScript 接口。说的简单明了一点就是让浏览器提供 JS 的即时通信接口。这个接口所创立的信道并不是像 WebSocket 一样，打通一个浏览器与 WebSocket 服务器之间的通信，而是通过一系列的信令，建立一个浏览器与浏览器之间（peer-to-peer）的信道，这个信道可以发送任何数据，而不需要经过服务器。并且 WebRTC 通过实现 MediaStream，通过浏览器调用设备的摄像头、话筒，使得浏览器之间可以传递音频和视频。WebRTC 有三个重要的部分：MediaStream、RTCPeerConnection、RTCDataChannel:

- MediaStream：通过设备的摄像头及话筒获得视频、音频的同步流

- PeerConnection: 用于构建点对点之间稳定、高效的流传输的组件

- DataChannel：能够使得浏览器之间(点对点)简历一个高吞吐量、低延时的信道，用于传输任何数据

## 实时网络传输优化

### TCP 与 UDP

在大规模实时多媒体传输网络中，TCP 和 RTMP 都不占优势。TCP 是个拥塞公平传输的协议，它的拥塞控制都是为了保证网络的公平性而不是快速到达，我们知道，TCP 层只有顺序到对应的报文才会提示应用层读数据，如果中间有报文乱序或者丢包都会在 TCP 做等待，所以 TCP 的发送窗口缓冲和重发机制在网络不稳定的情况下会造成延迟不可控，而且传输链路层级越多延迟会越大。

在实时传输中使用 UDP 更加合理，UDP 避免了 TCP 繁重的三次握手、四次挥手和各种繁杂的传输特性，只需要在 UDP 上做一层简单的链路 QoS 监测和报文重发机制，实时性会比 TCP 好，这一点从 RTP 和 DDCP 协议可以证明这一点，我们正式参考了这两个协议来设计自己的通信协议。

UDP 不可避免地存在抖动、乱序、丢包问题，视频必须按照严格是时间戳来播放，否则的就会出现视频动作加快或者放慢的现象，如果我们按照接收到视频数据就立即播放，那么这种加快和放慢的现象会非常频繁和明显。也就是说网络抖动会严重影响视频播放的质量，一般为了解决这个问题会设计一个视频播放缓冲区，通过缓冲接收到的视频帧，再按视频帧内部的时间戳来播放既可。

UDP 除了小范围的抖动以外，还是出现大范围的乱序现象，就是后发的报文先于先发的报文到达接收方。乱序会造成视频帧顺序错乱，一般解决的这个问题会在视频播放缓冲区里做一个先后排序功能让先发送的报文先进行播放。

UDP 在传输过程还会出现丢包，丢失的原因有多种，例如：网络出口不足、中间网络路由拥堵、socket 收发缓冲区太小、硬件问题、传输损耗问题等等。在基于 UDP 视频传输过程中，丢包是非常频繁发生的事情，丢包会造成视频解码器丢帧，从而引起视频播放卡顿。这也是大部分视频直播用 TCP 和 RTMP 的原因，因为 TCP 底层有自己的重传机制，可以保证在网络正常的情况下视频在传输过程不丢。基于 UDP 丢包补偿方式一般有以下几种：

- 报文冗余，报文冗余很好理解，就是一个报文在发送的时候发送 2 次或者多次。这个做的好处是简单而且延迟小，坏处就是需要额外 N 倍（N 取决于发送的次数）的带宽。

- FEC, Forward Error Correction，即向前纠错算法，常用的算法有纠删码技术（EC），在分布式存储系统中比较常见。最简单的就是 A B 两个报文进行 XOR（与或操作）得到 C，同时把这三个报文发往接收端，如果接收端只收到 AC,通过 A 和 C 的 XOR 操作就可以得到 B 操作。

- 丢包重传，丢包重传有两种方式，一种是 push 方式，一种是 pull 方式。Push 方式是发送方没有收到接收方的收包确认进行周期性重传，TCP 用的是 push 方式。pull 方式是接收方发现报文丢失后发送一个重传请求给发送方，让发送方重传丢失的报文。丢包重传是按需重传，比较适合视频传输的应用场景，不会增加太对额外的带宽，但一旦丢包会引来至少一个 RTT 的延迟。

### 拥塞控制

要评估一个网络通信质量的好坏和延迟一个重要的因素就是 Round-Trip Time（网络往返延迟）,也就是 RTT。评估两端之间的 RTT 方法很简单，大致如下：

- 发送端方一个带本地时间戳 T1 的 ping 报文到接收端；

- 接收端收到 ping 报文，以 ping 中的时间戳 T1 构建一个携带 T1 的 pong 报文发往发送端；

- 发送端接收到接收端发了的 pong 时，获取本地的时间戳 T2，用 T2 – T1 就是本次评测的 RTT。

因为客户端有可能在弱网环境下进行推流，音视频数据如果某一时刻发多了，就会引起网络拥塞或者延迟，如果发少了，可能视频的清晰不好。在实时音视频传输过程会设计一个自动适应本地网络变化的拥塞控制算法，像 QUIC 中的 BBR、webRTC 中 GCC 和通用的 RUDP。思路是通过 UDP 协议反馈的丢包和网络延迟(RTT)来计算当前网络的变化和最大瞬时吞吐量，根据这几个值调整上层的视频编码器的码率、视频分辨率等，从而达到适应当前网络状态的目的。

### QoS 策略

客户端推流除了需要考虑网络上传能力以外，还需要考虑客户端的计算能力。如果在 5 年前的安卓机上去编码一个分辨率为 640P 的高清视频流，那这个过程必然会产生延迟甚至无法工作。为此需要针对各个终端的计算能力设计一个 QoS 策略，不同计算能力的终端采用不同的视频编码器、分辨率、音频处理算法等，这个 QoS 策略会配合拥塞控制做一个状态不可逆的查找过程，直到找到最合适的 QoS 策略位置

## 媒体处理技术

### 回声消除

在实时音视频系统中，回声消除是一个难点，尽管 webRTC 提供了开源的回声消除模块，但在移动端和一些特殊的场景表现不佳。专业的实时音视频系统会进行回声消除的优化。回声消除的原理描述很简单，就是将扬声器播放的声音波形和麦克风录制的波形进行抵消，达到消除回声的作用。因为回声的回录时间不确定，所以很难确定什么时间点进行对应声音数据的抵消。在专业的回声消除模块里面通常会设计一个逼近函数，通过不断对输出和输入声音波形进行在线学习逼近，确定回声消除的时间差值点。

# 简单 Web 实验

本部分的代码实验参考 [MushiChat](https://github.com/wx-chevalier/MushiChat)。

## Media Source Extension

MSE 全称就是 Media Source Extensions。它是一套处理视频流技术的简称，里面包括了一系列 API：Media Source，Source Buffer 等。在没有 MSE 出现之前，前端对 video 的操作，仅仅局限在对视频文件的操作，而并不能对视频流做任何相关的操作。现在 MSE 提供了一系列的接口，使开发者可以直接提供 media stream。

```js
const vidElement = document.querySelector("video");

if (window.MediaSource) {
  const mediaSource = new MediaSource();
  vidElement.src = URL.createObjectURL(mediaSource);
  mediaSource.addEventListener("sourceopen", sourceOpen);
} else {
  console.log("The Media Source Extensions API is not supported.");
}

function sourceOpen(e) {
  URL.revokeObjectURL(vidElement.src);
  const mime = 'video/webm; codecs="opus, vp9"';
  const mediaSource = e.target;
  const sourceBuffer = mediaSource.addSourceBuffer(mime);
  const videoUrl = "droid.webm";
  fetch(videoUrl)
    .then(function (response) {
      return response.arrayBuffer();
    })
    .then(function (arrayBuffer) {
      sourceBuffer.addEventListener("updateend", function (e) {
        if (!sourceBuffer.updating && mediaSource.readyState === "open") {
          mediaSource.endOfStream();
        }
      });
      sourceBuffer.appendBuffer(arrayBuffer);
    });
}
```

其中 MediaSource 只是一系列视频流的管理工具，它可以将音视频流完整的暴露给 Web 开发者来进行相关的操作和处理。所以，它本身不会造成过度的复杂性。
