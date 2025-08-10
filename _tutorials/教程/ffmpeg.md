---
layout: post
title: "ffmpeg"
lesson: 2
category: 教程
---

ffmpeg是一款非常好用处理音视频的工具包。那什么是ffmpeg呢？FFmpeg是一套可以用来记录、转换数字音频、视频，并能将其转化为流的开源计算机程序，可以结合开发一些处理视频音频的功能。**1.ffmpeg下载**首先打开 [ffmpeg官网下载](https://link.segmentfault.com/?enc=q65RI2THCGPLMYh%2BOFiqhQ%3D%3D.YlRh94sVuAH3u6obXB4yVVais5bWGaT4b0qhcqAw34SLnqE1EDOs4ukMadjnDd2cCoBLMCuBNeK34hYj6aIJCg%3D%3D)然后点击 windows 对应的图标，再点击下面的”Windows EXE Files”随便选一个点进去选择一个版本下载。

**2.下载后解压，配置环境变量**下载解压后就能在 bin 文件夹下能看到三个可执行程序：ffmpeg、ffplay、ffprobe，配置好环境变量后即可使用。验证是否成功：cmd窗口输入ffmpeg -version 。如下图则安装成功。

**3.关键指令**一.查看FFmpeg支持的编码器

ffmpeg configure -encoders

二.查看FFmpeg支持的解码器

ffmpeg configure -decoders

三.查看FFmpeg支持的通信协议

ffmpeg configure -protocols

四.查看FFmpeg所支持的音视频编码格式、文件封装格式与流媒体传输协议

ffmpeg configure --help

五.播放视频[FFmpeg命令行工具学习(二)：播放媒体文件的工具ffplay](https://link.segmentfault.com/?enc=7riFRV3eV%2FAKWulgZDUXLQ%3D%3D.iQxDQIcyzSFT1hru5i7UnQUrP0ivjFnMMd7Wx7If6wTNzP9i22DPX%2B3SMcgl%2FRBT)

ffplay input.mp4
ffplay -autoexit input.mp4

六.设置视频的屏幕高宽比

ffmpeg -i input.mp4 -aspect 16:9 output.mp4```
通常使用的宽高比是：
16:9
4:3
16:10
5:4
2:21:1
2:35:1
2:39:1
```

七.编码格式转换MPEG4编码转成H264编码

ffmpeg -i input.mp4 -strict -2 -vcodec h264 output.mp4

H264编码转成MPEG4编码

ffmpeg -i input.mp4 -strict -2 -vcodec mpeg4 output.mp4

**4.视频压缩**

ffmpeg -i 2020.mp4 -vcodec h264 -vf scale=640:-2 -threads 4 2020_conv.mp4
ffmpeg -i 1579251906.mp4 -strict -2 -vcodec h264 1579251906_output.mp4

参数解释:

```
-i 2020.mp4
输入文件，源文件

2020_conv.mp4
输出文件，目标文件

-vf scale=640:-2  
改变视频分辨率，缩放到640px宽，高度的-2是考虑到libx264要求高度是偶数，所以设置成-2,让软件自动计算得出一个接近等比例的偶数高

-threads 4
4核运算
```

其他参数：

```
-s 1280x720 
设置输出文件的分辨率，w*h。

-b:v 
输出文件的码率，一般500k左右即可，人眼看不到明显的闪烁，这个是与视频大小最直接相关的。

-preset
指定输出的视频质量，会影响文件的生成速度，有以下几个可用的值 ultrafast, superfast, veryfast, faster, fast, medium, slow, slower, veryslow。
与 veryslow相比，placebo以极高的编码时间为代价，只换取了大概1%的视频质量提升。这是一种收益递减准则：slow 与 medium相比提升了5%~10%；slower 与 slow相比提升了5%；veryslow 与 slower相比提升了3%。
针对特定类型的源内容（比如电影、动画等），还可以使用-tune参数进行特别的优化。

-an
去除音频流。

-vn
去除视频流。

-c:a
指定音频编码器。

-c:v
指定视频编码器，libx264，libx265，H.262，H.264，H.265。
libx264：最流行的开源 H.264 编码器。
NVENC：基于 NVIDIA GPU 的 H.264 编码器。
libx265：开源的 HEVC 编码器。
libvpx：谷歌的 VP8 和 VP9 编码器。
libaom：AV1 编码器。

-vcodec copy
表示不重新编码，在格式未改变的情况采用。

-re 
以源文件固有帧率发送数据。

-minrate 964K -maxrate 3856K -bufsize 2000K 
指定码率最小为964K，最大为3856K，缓冲区大小为 2000K。

-y
不经过确认，输出时直接覆盖同名文件。

-crf
参数来控制转码，取值范围为 0~51，其中0为无损模式，18~28是一个合理的范围，数值越大，画质越差。
```

**5.视频拼接**一.将4个视频拼接成一个很长的视频（无声音）

ffmpeg -i 0.mp4 -i 1.mp4 -i 2.mp4 -i 3.mp4 -filter_complex '[0:0][1:0] [2:0][3:0] concat=n=4:v=1 [v]' -map '[v]' output.mp4

二.将4个视频拼接成一个很长的视频（有声音）

ffmpeg -i 1.mp4 -i 2.mp4 -i 3.mp4 -filter_complex '[0:0][0:1] [1:0][1:1] [2:0][2:1] concat=n=3:v=1:a=1 [v][a]' -map '[v]' -map '[a]’  output.mp4

参数解释：

```
[0:0][0:1] [1:0][1:1] [2:0][2:1] 
分别表示第1个输入文件的视频、音频，第2个输入文件的视频、音频，第3个输入文件的视频、音频。

concat=n=3:v=1:a=1 
表示有3个输入文件，输出一条视频流和一条音频流。

[v][a] 
得到的视频流和音频流的名字，注意在 bash 等 shell 中需要用引号，防止通配符扩展。
```

三.横向拼接2个视频

ffmpeg -i 0.mp4 -i 1.mp4 -filter_complex "[0:v]pad=iw*2:ih*1[a];[a][1:v]overlay=w" out.mp4

参数解释

```
pad
将合成的视频宽高，这里iw代表第1个视频的宽，iw*2代表合成后的视频宽度加倍，ih为第1个视频的高，合成的两个视频最好分辨率一致。

overlay
覆盖，[a][1:v]overlay=w，后面代表是覆盖位置w:0。
```

四.竖向拼接2个视频

ffmpeg -i 0.mp4 -i 1.mp4 -filter_complex "[0:v]pad=iw:ih*2[a];[a][1:v]overlay=0:h" out_2.mp4

五.横向拼接3个视频

ffmpeg -i 0.mp4 -i 1.mp4 -i 2.mp4 -filter_complex "[0:v]pad=iw*3:ih*1[a];[a][1:v]overlay=w[b];[b][2:v]overlay=2.0*w" out_v3.mp4

六.竖向拼接3个视频

ffmpeg -i 0.mp4 -i 1.mp4 -i 2.mp4 -filter_complex "[0:v]pad=iw:ih*3[a];[a][1:v]overlay=0:h[b];[b][2:v]overlay=0:2.0*h" out_v4.mp4

七.4个视频2x2方式排列

ffmpeg -i 0.mp4 -i 1.mp4 -i 2.mp4 -i 3.mp4 -filter_complex "[0:v]pad=iw*2:ih*2[a];[a][1:v]overlay=w[b];[b][2:v]overlay=0:h[c];[c][3:v]overlay=w:h" out.mp4

**6.视频帧操作**[ffmpeg和H264视频的编解码](https://link.segmentfault.com/?enc=1v4vNMjsSS2oy%2FKipqUmOQ%3D%3D.qxuk1u8MA2g2cqYbIXFYJPyj4Czy8d5v9yi%2F4XrE5oIf0Qu08xzFv3yBXFrj%2F5ww)

一.查看每帧的信息

ffprobe -v error -show_frames gemfield.mp4

从pict\_type=I可以看出这是个关键帧，然后key\_frame=1 表示这是IDR frame，如果key\_frame=0表示这是Non-IDR frame。

二.截取视频中的某一帧把gemfield.mp4视频的第1分05秒的一帧图像截取出来。

# input seeking
ffmpeg -ss 00:1:05 -i gemfield.mp4 -frames:v 1 out.jpg# output seeking
ffmpeg -i gemfield.mp4 -ss 00:1:05 -frames:v 1 out1.jpg

参数解释：

-frame:v 1，在video stream上截取1帧。
input seeking使用的是key frames，所以速度很快；而output seeking是逐帧decode，直到1分05秒，所以速度很慢。

重要说明：

ffmpeg截取视频帧有2种 seeking 方式，对应有2种 coding 模式：transcoding 和 stream copying（ffmpeg -c copy）。
transcoding 模式：需要 decoding + encoding 的模式，即先 decoding 再encoding。
stream copying 模式：不需要decoding + encoding的模式，由命令行选项-codec加上参数copy来指定（-c:v copy ）。在这种模式下，ffmpeg在video stream上就会忽略 decoding 和 encoding步骤。

三.查看视频总帧数

ffprobe -v error -count_frames -select_streams v:0 -show_entries stream=nb_frames -of default=nokey=1:noprint_wrappers=1 gemfield.mp4

四.查看 key frame 帧数

ffprobe -v error -count_frames -select_streams v:0 -show_entries stream=nb_read_frames -of default=nokey=1:noprint_wrappers=1 -skip_frame nokey gemfield.mp4

五.查看 key frame 所在的时间

ffprobe -v error -skip_frame nokey -select_streams v:0 -show_entries frame=pkt_pts_time -of csv=print_section=0 gemfield.mp4

六.查看 key frame 分布的情况

ffprobe -v error -show_frames gemfield.mp4 | grep pict_type

七.查看 key frame 所在的帧数

ffprobe -v error -select_streams v -show_frames -show_entries frame=pict_type -of csv gemfield.mp4 | grep -n I | cut -d ':' -f 1

八.重新设置 key frame interval

ffmpeg -i gemfield.mp4 -vcodec libx264 -x264-params keyint=1:scenecut=0 -acodec copy out.mp4

九.查看视频波特率

ffprobe -v error -select_streams v:0 -show_entries stream=bit_rate -of default=noprint_wrappers=1:nokey=1 gemfield.mp4

**7.图片与视频**

7.1 图片转视频（规则的名称）

ffmpeg -f image2 -i 'in%6d.jpg' -vcodec libx264 -r 25 -b 200k test.mp4

参数解释：

-r 25 表示每秒播放25帧
-b 200k 指定码率为200k
图片的文件名为"in000000.jpg"，从0开始依次递增。

7.2 图片转视频（不规则的名称）不规则图片名称转视频。7.2.1 方法一不规则图片名称合成视频文件。

```
ffmpeg -framerate 10 -pattern_type glob -i '*.jpg' out.mp4

cat *.png | ffmpeg -f image2pipe -i - output.mp4

参数解释：
-framerate 10：视频帧率
-pattern_type glob：Glob pattern 模糊匹配
-f image2pipe：图像管道，模糊匹配得到图片名称
```

7.2.2 方法二不规则图片名称合成视频文件。一.先动手把不规则文件重命名规则图片名。

```
def getTpyeFile(filelist, type):     
    res = []     
    for item in filelist:
         name, suf = os.path.splitext(item) 
         if suf == type:
             res.append(item)
     return res

pwd = os.getcwd() 
dirs = os.listdir() 
typefiles = getTpyeFile(dirs, '.jpg')

for i in range(0,len(typefiles)):
     os.rename(typefiles[i],"./%d.jpg" % (i))
```

二.将需要合成的图片放在txt中，通过读取txt文件合并成视频。

ffmpeg -f concat -i files.txt output.mp4

7.3 图片格式转换[ffmpeg图片格式转换](https://link.segmentfault.com/?enc=vkHQ%2BEkjio90gTNVUP4Sbg%3D%3D.kObPLYzD4vRaOubC52kyZCyy75RC41GjvibotjUZKclPUiIuYEyM4G26ncRfDcZiAICVwZpfFfB%2FNwVGfvnknQ%3D%3D)

webp转换成jpg

ffmpeg -i in.webp out.jpg

webp转换成png

ffmpeg -i in.webp out.png

jpg转换成png

ffmpeg -i in.jpg out.png

jpg转换成webp

ffmpeg -i in.jpg out.webp

png转换成webp

ffmpeg -i in.png out.webp

png转换成jpg

ffmpeg -i in.png out.jpg

**8、硬解码与软解码**一.CPU富余、需要精准控制解码流程、有解码算法的优化、通用性要求高，直接使用软解（也就是CPU解码）;二.有其他编解码芯片/模组、CPU不够用，就不得不需要转向硬解码（也就是专用芯片解码）。

2022-09-13 新增[ffmpeg命令目录](https://link.segmentfault.com/?enc=4i4%2FQu4S0wp9bje6LuGUkw%3D%3D.cTjLjpqVYaEn6x2ySdcce9eil99HeEh6gtuq2fPk3xPeBvF6rotyHU0uBcdnyIz7dpGtWYmUqqBFsRn8kaGNtg%3D%3D)

**调整视频分辨率-s**

```
1、用-s参数设置视频分辨率，参数值wxh，w宽度单位是像素，h高度单位是像素
ffmpeg -i input_file -s 320x240 output_file

2、预定义的视频尺寸
    下面两条命令有相同效果
    ffmpeg -i input.avi -s 640x480 output.avi
    ffmpeg -i input.avi -s vga output.avi
```

**Scale filter调整分辨率**

```
Scale filter的优点是可以使用一些额外的参数
    Scale=width:height[:interl={1|-1}]

下面两条命令有相同效果
    ffmpeg -i input.mpg -s 320x240 output.mp4 
    ffmpeg -i input.mpg -vf scale=320:240 output.mp4

对输入视频成比例缩放
改变为源视频一半大小
    ffmpeg -i input.mpg -vf scale=iw/2:ih/2 output.mp4
改变为原视频的90%大小：
    ffmpeg -i input.mpg -vf scale=iw*0.9:ih*0.9 output.mp4
```

**在未知视频的分辨率时，保证调整的分辨率与源视频有相同的横纵比。**可能会有错误，不推荐使用，最好传入明确的缩放值另外，scale只能接受偶数，否则height not divisible by 2

```
宽度固定400，高度成比例：
    ffmpeg -i input.avi -vf scale=400:-2

相反地，高度固定300，宽度成比例：
    ffmpeg -i input.avi -vf scale=-2:300
```