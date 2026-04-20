# FFmpeg CheatSheet

# 基础使用

FFmpeg 可以使用下面的参数进行基本信息查询。例如，想查询一下现在使用的 FFmpeg 都支持哪些 filter，就可以用 ffmpeg -filters 来查询。详细参数说明如下：

| 命令            | 作用                                 |
| --------------- | ------------------------------------ |
| ffmpeg -version | 显示版本                             |
| -formats        | 显示可用的格式（包括设备）           |
| -demuxers       | 显示可用的 demuxers                  |
| -muxers         | 显示可用的 muxers                    |
| -devices        | 显示可用的设备                       |
| -codecs         | 显示已知的所有编解码器               |
| -decoders       | 显示可用的解码器                     |
| -encoders       | 显示所有可用的编码器                 |
| -bsfs           | 显示可用的比特流 filter              |
| -protocols      | 显示可用的协议                       |
| -filters        | 显示可用的过滤器                     |
| -pix_fmts       | 显示可用的像素格式                   |
| -sample_fmts    | 显示可用的采样格式                   |
| -layouts        | 显示 channel 名称和标准 channel 布局 |
| -colors         | 显示识别的颜色名称                   |

## 参数

```sh
# Common switches
-codecs          # list codecs
-c:v             # video codec (-vcodec): 'copy' to copy stream
-c:a             # audio codec (-acodec)
-fs SIZE         # limit file size (bytes)

# Audio
-aq QUALITY      # audio quality (codec-specific)
-ar 44100        # audio sample rate (hz)
-ac 1            # audio channels (1=mono, 2=stereo)
-an              # no audio
-vol N           # volume (256=normal)

# Bitrate
-b:v 1M          # video bitrate (1M = 1Mbit/s)
-b:a 1M          # audio bitrate

# Video
-aspect RATIO    # aspect ratio (4:3, 16:9, or 1.25)
-r RATE          # frame rate per sec
-s WIDTHxHEIGHT  # frame size
-vn              # no video
```

# 录制

```sh
# 查找设备名

## Windows
$ ffmpeg -list_devices true -f dshow -i dummy

## MAC
$ ffmpeg -f avfoundation -list_devices true -i ""
```

## Windows

```go
$ ffmpeg -f dshow -i video="Virtual-Camera" -preset ultrafast -vcodec libx264 -tune zerolatency -b 900k -f mpegts udp://10.1.0.102:1234

$ ffmpeg -f dshow -i video="screen-capture-recorder":audio="Stereo Mix (IDT High Definition" \
-vcodec libx264 -preset ultrafast -tune zerolatency -r 10 -async 1 -acodec libmp3lame -ab 24k -ar 22050 -bsf:v h264_mp4toannexb \
-maxrate 750k -bufsize 3000k -f mpegts udp://192.168.5.215:48550
```

- `-f fshow`: windows system drivers for capturing video and audio
- `-f v4l2`: linux system drivers for capturing video
- `-f alsa`: linux system drivers for capturing audio
- `-i`: ffmpeg option that defines **input**
- `-vcodec libx264`: raw video from camera will be encoded using H264 video codec
- `-r 10`: video FPS (frames per second)
- `-b:v 512k`: video bitrate Kb/s (kilo bits per second)
- `-s 640x360`: video width and height
- `-acodec aac`: raw audio from microphone will be encoded using AAC audio codec
- `-ac 2`: 2 audio channels (stereo)
- `-ab 32k`: audio bitrate in Kb/s
- `-ar 44100`: audio sampling rate 44.1 KHz
- `-f mpegts`: video and audio will be packed into [MPEG transport stream (MPEG TS)](https://en.wikipedia.org/wiki/MPEG_transport_stream)
- `udp://192.168.1.4:5000`: MPEG transport stream is sent via UDP protocol to computer with IP address 192.168.1.4 on IP port 5000.

```sh
$ ffmpeg -y -loglevel warning -f dshow -i video="screen-capture-recorder" -vf crop=690:388:136:0 -r 30 -s 962x388 -threads 2 -vcodec libx264 -vpre baseline -vpre my_ffpreset -f flv rtmp:///live/myStream.sdp

# 输出为 MP4
$ ffmpeg -f dshow -rtbufsize 1000000k -s 640×480 -r 30 -i video=”1714-INOGENI 4K2USB3″ -an -c:v libx264 -q 0 -f h264 – | ffmpeg -f h264 -i – -an -c:v copy -f mp4 file.mp4 -an -c:v copy -f h264 pipe:play | ffplay -i pipe:play
```

屏幕录制：

```sh
# 屏幕录制并保存成文件
$ ffmpeg -f gdigrab -i desktop eguid.mp4

# 屏幕录制并推流
$ ffmpeg -f gdigrab -i desktop -vcodec libx264 -preset:v ultrafast -tune:v zerolatency -f flv rtmp://eguid.cc:1935/rtmp/destop

# 视频文件推流
$ ffmpeg -re -i eguid.flv -vcodec copy -acodec copy -f flv -y rtmp://eguid.cc:1935/rtmp/eguid

# 转流（rtsp转rtmp为例）
$ ffmpeg -i rtsp://184.72.239.149/vod/mp4://BigBuckBunny_175k.mov -rtsp_transport tcp -vcodec h264 -acodec aac -f flv rtmp://eguid.cc:1935/rtmp/eguid

# 拉流

- ffmpeg -i rtmp://eguid.cc:1935/rtmp/eguid -vcodec h264 -f flv -acodec aac -ac 2 eguid.flv
```

## Mac

```sh
# 录屏+声音
$ ffmpeg -f avfoundation -i 1 -r 30 out.yuv
-f 指定使用 avfoundation 采集数据。
-i 指定从哪儿采集数据，它是一个文件索引号。在我的MAC上，1代表桌面（可以通过上面的命令查询设备索引号）。
-r 指定帧率。按ffmpeg官方文档说-r与-framerate作用相同，但实际测试时发现不同。-framerate 用于限制输入，而-r用于限制输出。

# 录视频
$ ffmpeg -f avfoundation -i 1:0 -r 29.97 -c:v libx264 -crf 0 -c:a libfdk_aac -profile:a aac_he_v2 -b:a 32k out.flv
-i 1:0 冒号前面的 “1” 代表的屏幕索引号。冒号后面的"0"代表的声音索相号。
-c:v 与参数 -vcodec 一样，表示视频编码器。c 是 codec 的缩写，v 是video的缩写。
-crf 是 x264 的参数。0 表式无损压缩。
-c:a 与参数 -acodec 一样，表示音频编码器。
-profile 是 fdk_aac 的参数。aac_he_v2 表式使用 AAC_HE v2 压缩数据。
-b:a 指定音频码率。b 是 bitrate的缩写, a是 audio的缩与。

# 录音
$ ffmpeg -f avfoundation -i :0 out.wav
# 录制音频裸数据
$ ffmpeg -f avfoundation -i :0 -ar 44100 -f s16le out.pcm
```

```sh
#! /bin/bash
#
# Diffusion bilibili live avec ffmpeg
# Make sure you have FFmpeg installed in your mac

# list avfoundation devices
ffmpeg -f avfoundation -list_devices true -i ""

# change the param after `-i` and `-f flv`

# use 140m mermory
ffmpeg \
  -f avfoundation \
  -re -i "2" \
  -vcodec libx264 \
  -preset ultrafast \
  -acodec aac \
  -ar 44100 \
  -ac 1 \
  -f flv "rtmp://example.com/path?key=xx"

# 560m mermory 90% cpu
ffmpeg \
  -f avfoundation \
  -video_size 1920x1080 \
  -framerate 30 \
  -i "2:0" -ac 2 \
  -vcodec libx264 -maxrate 2000k \
  -bufsize 2000k -acodec libmp3lame -ar 44100 -b:a 128k \
  -f flv "rtmp://example.com/path?key=xx"
```

## 其他直播

- 推流: `ffmpeg -re -i out.mp4 -c copy -f flv rtmp://server/live/streamName`

- 拉流保存: `ffmpeg -i rtmp://server/live/streamName -c copy dump.flv`

- 转流: `ffmpeg -i rtmp://server/live/originalStream -c:a copy -c:v copy -f flv rtmp://server/live/h264Stream`

- 实时推流: `ffmpeg -framerate 15 -f avfoundation -i "1" -s 1280x720 -c:v libx264 -f flv rtmp://localhost:1935/live/room`

# 视频处理

```sh
$ ffmpeg -framerate 1 -pattern_type glob -i '*.bmp' -c:v libx264 -r 30 -pix_fmt yuv420p out.mp4
```

## 视频联接

```sh
:: Create File List
echo file file1.mp4 >  mylist.txt
echo file file2.mp4 >> mylist.txt
echo file file3.mp4 >> mylist.txt

# Windows 下视频连接
:: Concatenate Files
$ ffmpeg -f concat -i mylist.txt -c copy output.mp4

:: Create File List
for %%i in (*.mp4) do echo file '%%i'>> mylist.txt

:: Concatenate Files
$ ffmpeg -f concat -safe 0 -i mylist.txt -c copy output.mp4

$ ffmpeg -f avfoundation -i "1" -framerate 30 -f avfoundation -i "0:0" -r 30 -c:v libx264 -preset ultrafast -c:a libfdk_aac -profile:a aac_he_v2 -ar 44100 -ac 2 -filter_complex "[0:v]scale=320:240[a];[a]pad=640:240[b];[b][1:v]overlay=320:0[out]" -map "[out]" -movflags faststart -map 1:a c.mp4
```

## 分解/复用

- **抽取音频流**

`ffmpeg -i input.mp4 -acodec copy -vn out.aac`

acodec: 指定音频编码器，copy 指明只拷贝，不做编解码。
vn: v 代表视频，n 代表 no 也就是无视频的意思。

- **抽取视频流**

`ffmpeg -i input.mp4 -vcodec copy -an out.h264`

vcodec: 指定视频编码器，copy 指明只拷贝，不做编解码。
an: a 代表视频，n 代表 no 也就是无音频的意思。

- **转格式**

`ffmpeg -i out.mp4 -vcodec copy -acodec copy out.flv`

上面的命令表式的是音频、视频都直接 copy，只是将 mp4 的封装格式转成了 flv。

- **音视频合并**

`ffmpeg -i out.h264 -i out.aac -vcodec copy -acodec copy out.mp4`

## 格式转换与压缩

```sh
$ ffmpeg -i in.mp4 out.avi
```

```sh
$ ffmpeg -i foo.mp3 -ac 1 -ab 128000 -f mp4 -acodec libfaac -y target.m4r

# no audio
ffmpeg -i input.mov -vcodec h264   -an -strict -2 output.mp4
ffmpeg -i input.mov -vcodec libvpx -an output.webm
ffmpeg -i input.mov -vcodec h264 -acodec aac -strict -2 output.mp4
ffmpeg -i input.mov -vcodec libvpx -acodec libvorbis output.webm
<video width="320" height="240" controls>
  <source src="movie.mp4" type='video/mp4'></source>
  <source src="movie.webm" type='video/ogg'></source>
</video>
```

- 视频缩小一倍

```sh
$ ffmpeg -i out.mp4 -vf scale=iw/2:-1 scale.mp4
```

`-vf scale` 指定使用简单过滤器 scale，iw/2:-1 中的 iw 指定按整型取视频的宽度。-1 表示高度随宽度一起变化。

- 视频裁剪

```sh
$ ffmpeg -i VR.mov -vf crop=in_w-200:in_h-200 -c:v libx264 -c:a copy -video_size 1280x720 vr_new.mp4
```

crop 格式：crop=out_w:out_h: x :y

- out_w: 输出的宽度。可以使用 in_w 表式输入视频的宽度。
- out_h: 输出的高度。可以使用 in_h 表式输入视频的高度。
- x : X 坐标
- y : Y 坐标

- 倍速播放

```sh
$ ffmpeg -i out.mp4 -filter_complex "[0:v]setpts=0.5*PTS[v];[0:a]atempo=2.0[a]" -map "[v]" -map "[a]" speed2.0.mp4
```

- -filter_complex 复杂滤镜，[0:v]表示第一个（文件索引号是 0）文件的视频作为输入。`setpts=0.5*PTS` 表示每帧视频的 pts 时间戳都乘 0.5，也就是差少一半。[v]表示输出的别名。音频同理就不详述了。
- map 可用于处理复杂输出，如可以将指定的多路流输出到一个输出文件，也可以指定输出到多个文件。"[v]" 复杂滤镜输出的别名作为输出文件的一路流。上面 map 的用法是将复杂滤镜输出的视频和音频输出到指定文件中。

### 图/视互转

- **视频转 JPEG**：`ffmpeg -i test.flv -r 1 -f image2 image-%3d.jpeg`

- **视频转 gif**：`ffmpeg -i out.mp4 -ss 00:00:00 -t 10 out.gif`

- **图片转视频**：`ffmpeg -f image2 -i image-%3d.jpeg images.mp4`

## 对称视频与画中画

- 对称视频：`$ ffmpeg -i out.mp4 -filter_complex "[0:v]pad=w=2*iw[a];[0:v]hflip[b];[a][b]overlay=x=w" duicheng.mp4`

- 画中画：`ffmpeg -i out.mp4 -i out1.mp4 -filter_complex "[1:v]scale=w=176:h=144:force_original_aspect_ratio=decrease[ckout];[0:v][ckout]overlay=x=W-w-10:y=0[out]" -map "[out]" -movflags faststart new.mp4`

- 录制画中画：`ffmpeg -f avfoundation -i "1" -framerate 30 -f avfoundation -i "0:0" -r 30 -c:v libx264 -preset ultrafast -c:a libfdk_aac -profile:a aac_he_v2 -ar 44100 -ac 2 -filter_complex "[1:v]scale=w=176:h=144:force_original_aspect_ratio=decrease[a];[0:v][a]overlay=x=W-w-10:y=0[out]" -map "[out]" -movflags faststart -map 1:a b.mp4`

## 处理原始数据

- **提取 YUV 数据**

`ffmpeg -i input.mp4 -an -c:v rawvideo -pixel_format yuv420p out.yuv ffplay -s wxh out.yuv`

-c:v rawvideo 指定将视频转成原始数据
-pixel_format yuv420p 指定转换格式为 yuv420p

- **YUV 转 H264**

`ffmpeg -f rawvideo -pix_fmt yuv420p -s 320x240 -r 30 -i out.yuv -c:v libx264 -f rawvideo out.h264`

- **提取 PCM 数据**

`ffmpeg -i out.mp4 -vn -ar 44100 -ac 2 -f s16le out.pcm ffplay -ar 44100 -ac 2 -f s16le -i out.pcm`

# 滤镜

在编码之前，ffmpeg 可以使用 libavfilter 库中的过滤器处理原始音频和视频帧。几个链式过滤器形成一个过滤器图形。ffmpeg 区分两种类型的过滤器图形：简单和复杂。

## 水印

- 添加水印

`ffmpeg -i out.mp4 -vf "movie=logo.png,scale=64:48[watermask];[in][watermask] overlay=30:10 [out]" water.mp4`

`-vf` 中的 movie 指定 logo 位置。scale 指定 logo 大小。overlay 指定 logo 摆放的位置。

- 滤镜加水印

`ffmpeg -i killer.mp4 -filter_complex "movie=./logo/daka.png,scale=64:48[w];[0:v]curves=vintage[o];[o][w]overlay=30:10[out]" -map "[out]" -map 0:a test1.mp4`

- 删除水印

先通过 ffplay 找到要删除 LOGO 的位置。

```sh
$ ffplay -i test.flv -vf delogo=x=806:y=20:w=70:h=80:show=1
```

使用 delogo 滤镜删除 LOGO。

```sh
$ ffmpeg -i test.flv -vf delogo=x=806:y=20:w=70:h=80 output.flv
```
