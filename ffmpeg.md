# FFMPEG

[TOC]

## 用法

`ffmpeg [options] [[infile options] -i infile]... {[outfile options] outfile}...`

获取帮助：

| 选项           | 说明                                       |
| ------------ | ---------------------------------------- |
| -h           | 打印基本选项                                   |
| -h long      | 打印更多选项                                   |
| -h full      | 打印所有选项（包括所有格式和编解码器特定选项，很长）               |
| -h type=name | 打印命名的decode / encoder / demuxer / muxer / filter的所有选项 |

有关选项的详细说明，请参阅man ffmpeg。

### 打印帮助/信息/功能：

| 选项              | 说明          |
| --------------- | ----------- |
| -L              | 展示许可证       |
| -h topic        | 显示帮助        |
| -? topic        | 显示帮助        |
| -help topic     | 显示帮助        |
| --help topic    | 显示帮助        |
| -version        | 显示版本        |
| -buildconf      | 显示构建配置      |
| -formats        | 显示可用的格式     |
| -muxers         | 显示可用的复用器    |
| -demuxers       | 显示可用的分离器    |
| -devices        | 显示可用设备      |
| -codecs         | 显示可用的编解码器   |
| -decoders       | 显示可用的解码器    |
| -encoders       | 显示可用的编码器    |
| -bsfs           | 显示可用的位流过滤器  |
| -protocols      | 显示可用的协议     |
| -filters        | 显示可用的过滤器    |
| -pix_fmts       | 显示可用的像素格式   |
| -layouts        | 显示标准通道布局    |
| -sample_fmts    | 显示可用的音频样本格式 |
| -colors         | 显示可用的颜色名称   |
| -sources device | 列出输入设备的源    |
| -sinks device   | 列表输出设备的接收器  |
| -hwaccels       | 显示可用的硬件加速方法 |
### 全局选项（影响整个程序而不是单个文件：

| 选项                       | 说明                          |
| ------------------------ | --------------------------- |
| -loglevel loglevel       | 设置日志级别                      |
| -v loglevel              | 设置日志级别                      |
| -report                  | 生成报告                        |
| -max_alloc bytes         | 设置单个分配块的最大大小                |
| -y                       | 覆盖输出文件                      |
| -n                       | 永远不会覆盖输出文件                  |
| -ignore_unknown          | 忽略未知流类型                     |
| -filter_threads          | 非复杂过滤线程数                    |
| -filter_complex_threads  | -filter_complex的线程数         |
| -stats                   | 在编码期间打印进度报告                 |
| -max_error_rate ratio of | 错误率（0.0：无错误，1.0：100％错误最大错误率 |
| -bits_per_raw_sample     | 设置每个原始样本的位数                 |
| -vol volume              | 改变音量（256 =正常）               |

### 每个文件主要选项

| 选项                                       | 说明                                       |
| ---------------------------------------- | ---------------------------------------- |
| -f fmt                                   | 强制格式                                     |
| -c codec                                 | 编解码器名称                                   |
| -codec codec                             | 编解码器名称                                   |
| -pre preset                              | 预设名称                                     |
| -map_metadata outfile[,metadata]:infile[,metadata] | 从infile设置outfile的元数据信息                   |
| -t duration                              | 记录或转码音频/视频的“持续时间”秒                       |
| -to time_stop                            | 记录或转码停止时间                                |
| -fs limit_size                           | 设置限制文件大小（以字节为单位）                         |
| -ss time_off                             | 设置开始时间偏移量                                |
| -sseof time_off                          | 设置相对于EOF的开始时间偏移量                         |
| -seek_timestamp                          | 启用/禁用使用-ss查询时间戳                          |
| -timestamp time                          | 设置录制时间戳（'now'设置当前时间）                     |
| -metadata string=string                  | 添加元数据                                    |
| -program title=string:st=number...       | 添加指定流的程序                                 |
| -target type                             | 指定目标文件类型（“vcd”，“svcd”，“dvd”，“dv”或“dv50”, 可选前缀“pal-”，“ntsc-”或“film-”） |
| -apad                                    | 音频垫                                      |
| -frames number                           | 设置要输出的帧数                                 |
| -filter filter_graph                     | 设置流过滤器                                   |
| -filter_script filename                  | 从文件读取流过滤器描述                              |
| -reinit_filter                           | 重新输入输入参数更改的过滤器                           |
| -discard                                 | 丢弃                                       |
| -disposition                             | 处置                                       |

### 视频选项

| 选项                          | 说明                             |
| --------------------------- | ------------------------------ |
| -vframes number             | 设置要输出的视频帧数                     |
| -r rate                     | 设置帧速率（Hz值，分数或缩写）               |
| -s size                     | 设置帧大小（WxH或缩写）                  |
| -aspect aspect              | 设置纵横比（4：3, 16：9或1.3333，1.7777） |
| -bits_per_raw_sample number | 设置每个原始样本的位数                    |
| -vn                         | 禁用视频                           |
| -vcodec codec               | 强制视频编解码器（'复制'复制流）              |
| -timecode hh:mm:ss[:;.]ff   | 设置初始TimeCode值。                 |
| -pass n                     | 选择过程号码（1到3）                    |
| -vf filter_graph            | 设置视频过滤器                        |
| -ab bitrate                 | 音频比特率（请使用-b：a）                 |
| -b bitrate                  | 视频比特率（请使用-b：v）                 |
| -dn                         | 禁用数据                           |

### 音频选项

| 选项               | 说明                |
| ---------------- | ----------------- |
| -aframes number  | 设置要输出的音频帧数        |
| -aq quality      | 设置音频质量（编解码器专用）    |
| -ar rate         | 设置音频采样率（Hz）       |
| -ac channels     | 设置音频通道数           |
| -an              | 禁用音频              |
| -acodec codec    | 强制音频编解码器（'复制'复制流） |
| -vol volume      | 改变音量（256 =正常）     |
| -af filter_graph | 设置音频过滤器           |

### 字幕选项

| 选项                | 说明                |
| ----------------- | ----------------- |
| -s size           | 设置帧大小（WxH或缩写）     |
| -sn               | 禁用字幕              |
| -scodec codec     | 强制字幕编解码器（'复制'复制流） |
| -stag fourcc/tag  | 强制字幕标签/ 4cc       |
| -fix_sub_duration | 修复字幕持续时间          |
| -canvas_size size | 设置画布大小（WxH或缩写）    |
| -spre preset      | 将字幕选项设置为指定的预设     |

## 视频/音频编码

`copy`使用原本的编码

#### 视频编码

* libx264

* prores ` -vcodec prores -profile:v 数字`

  数字:

  0 : ProRes422 (Proxy)

  1 : ProRes422 (LT)

  2 : ProRes422 (Normal)

  3 : ProRes422 (HQ)

#### 音频编码

* libmp3lame 

## -preset

* ultrafast
* superfast
* veryfast
* faster
* fast
* medium
  * 默认值
* slow
* slower
* veryslow
* placebo

### Mp4格式自定义尺寸报错解决办法

是因为mp4格式只支持偶数尺寸, 增加以下选项:

```
-vf scale=trunc(iw/2)*2:trunc(ih/2)*2
```
