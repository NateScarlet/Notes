[TOC]

# FFMPEG

usage(用法):

`ffmpeg [options] [[infile options] -i infile]... {[outfile options] outfile}...`

获取帮助：

| 选项           | 说明                                       |
| ------------ | ---------------------------------------- |
| -h           | 打印基本选项                                   |
| -h long      | 打印更多选项                                   |
| -h full      | 打印所有选项（包括所有格式和编解码器特定选项，很长）               |
| -h type=name | 打印命名的decode / encoder / demuxer / muxer / filter的所有选项 |

有关选项的详细说明，请参阅man ffmpeg。

## 打印帮助/信息/功能

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
## 全局选项

影响整个程序而不是单个文件

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

## 每文件主选项

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

## 视频选项

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

## 音频选项

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

## 字幕选项

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

### 视频编码

* libx264

  mp4高质压缩编码

* prores ` -vcodec prores -profile:v 数字`

  数字:

  0 : ProRes422 (Proxy)

  1 : ProRes422 (LT)

  2 : ProRes422 (Normal)

  3 : ProRes422 (HQ) (合成素材常用它)

### 音频编码

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

是因为mp4格式只支持偶数尺寸, 增加以下选项即可解决:

```
-vf scale=trunc(iw/2)*2:trunc(ih/2)*2
```

## 过滤器详表

T.. =时间线支持
.S. =切片线程
..C =命令支持
   A =音频输入/输出
   V =视频输入/输出
   N =动态数字和/或输入/输出类型
   | =源或汇滤波器

| 特性   | 名称                | 用途            | 说明                                       |
| ---- | ----------------- | ------------- | ---------------------------------------- |
| ...  | abench            | `A->A       ` | 过滤器的基准部分。                                |
| ...  | acompressor       | `A->A       ` | 音频压缩机                                    |
| ...  | acrossfade        | `AA->A      ` | 交叉淡入两声输入音频流。                             |
| ...  | acrusher          | `A->A       ` | 降低音频位分辨率。                                |
| T..  | adelay            | `A->A       ` | 延迟一个或多个音频通道。                             |
| ...  | aecho             | `A->A       ` | 添加回音到音频。                                 |
| ...  | aemphasis         | `A->A       ` | 音频强调。                                    |
| ...  | aeval             | `A->A       ` | 根据指定的表达式过滤音频信号。                          |
| T..  | afade             | `A->A       ` | 淡入/淡出输入音频。                               |
| ...  | afftfilt          | `A->A       ` | 对频域中的样本应用任意表达式。                          |
| ...  | aformat           | `A->A       ` | 将输入音频转换为指定格式之一。                          |
| ...  | agate             | `A->A       ` | 音频门。                                     |
| ...  | ainterleave       | `N->A       ` | 时间交错音频输入。                                |
| ...  | alimiter          | `A->A       ` | 音频前视限幅器                                  |
| ...  | allpass           | `A->A       ` | 应用两极全通滤波器。                               |
| ...  | aloop             | `A->A       ` | 循环音频样本。                                  |
| ...  | amerge            | `N->A       ` | 将两个或多个音频流合并到单个多声道流中。                     |
| T..  | ametadata         | `A->A       ` | 操纵音频帧元数据。                                |
| ...  | amix              | `N->A       ` | 音频混音。                                    |
| ..C  | anequalizer       | `A->N       ` | 应用高阶音频参数多频段均衡器。                          |
| ...  | anull             | `A->A       ` | 将源传递给输出。                                 |
| T..  | apad              | `A->A       ` | 垫声音沉默。                                   |
| ...  | aperms            | `A->A       ` | 设置输出音频帧的权限。                              |
| ...  | aphaser           | `A->A       ` | 为音频添加相位效果。                               |
| ...  | apulsator         | `A->A       ` | 音频波轮                                     |
| ...  | arealtime         | `A->A       ` | 减慢过滤以实时匹配。                               |
| ...  | aresample         | `A->A       ` | 重新采样音频数据。                                |
| ...  | areverse          | `A->A       ` | 反转音频剪辑。                                  |
| ...  | aselect           | `A->N       ` | 选择音频帧传递输出。                               |
| ...  | asendcmd          | `A->A       ` | 发送命令到过滤器。                                |
| ...  | asetnsamples      | `A->A       ` | 设置每个输出音频帧的样本数。                           |
| ...  | asetpts           | `A->A       ` | 设置输出音频帧的PTS。                             |
| ...  | asetrate          | `A->A       ` | 更改采样率而不更改数据。                             |
| ...  | asettb            | `A->A       ` | 设置音频输出链接的时基。                             |
| ...  | ashowinfo         | `A->A       ` | 显示每个音频帧的文本信息。                            |
| T..  | asidedata         | `A->A       ` | 操纵音频帧端数据。                                |
| ...  | asplit            | `A->N       ` | 将音频输入传送到N个音频输出。                          |
| ...  | astats            | `A->A       ` | 显示有关音频帧的时域统计信息。                          |
| ..C  | astreamselect     | `N->N       ` | 选择音频流                                    |
| ..C  | atempo            | `A->A       ` | 调整音频速度                                   |
| ...  | atrim             | `A->A       ` | 从输入中选择一个连续的部分，放下其余部分。                    |
| ...  | bandpass          | `A->A       ` | 应用双极巴特沃斯带通滤波器。                           |
| ...  | bandreject        | `A->A       ` | 应用双极巴特沃斯滤波器。                             |
| ...  | bass              | `A->A       ` | 提升或削减较低的频率。                              |
| ...  | biquad            | `A->A       ` | 应用给定系数的双二阶IIR滤波器。                        |
| ...  | bs2b              | `A->A       ` | 鲍尔立体声到双耳滤波器。                             |
| ...  | channelmap        | `A->A       ` | 重新配置音频通道。                                |
| ...  | channelsplit      | `A->N       ` | 将音频分割为每通道流。                              |
| ...  | chorus            | `A->A       ` | 为音频添加合唱效果。                               |
| ...  | compand           | `A->A       ` | 压缩或扩展音频动态范围。                             |
| ...  | compensationdelay | `A->A       ` | 音频补偿延迟线。                                 |
| ...  | crystalizer       | `A->A       ` | 简单扩展音频动态范围过滤器。                           |
| T..  | dcshift           | `A->A       ` | 对音频应用直流偏移。                               |
| ...  | dynaudnorm        | `A->A       ` | 动态音频规格器。                                 |
| ...  | earwax            | `A->A       ` | 扩大立体图像。                                  |
| ...  | ebur128           | `A->N       ` | EBU R128扫描仪                              |
| ...  | equalizer         | `A->A       ` | 应用两极峰值均衡（EQ）滤波器。                         |
| ...  | extrastereo       | `A->A       ` | 增加立体声音频通道之间的差异。                          |
| ..C  | firequalizer      | `A->A       ` | 有限脉冲响应均衡器。                               |
| ...  | flanger           | `A->A       ` | 对音频应用折边效果。                               |
| ...  | hdcd              | `A->A       ` | 应用高分辨率兼容数字（HDCD）解码。                      |
| ...  | highpass          | `A->A       ` | 应用3dB点频率的高通滤波器。                          |
| ...  | join              | `N->A       ` | 将多个音频流连接到多声道输出。                          |
| ...  | loudnorm          | `A->A       ` | EBU R128响度归一化                            |
| ...  | lowpass           | `A->A       ` | 应用3dB点频率的低通滤波器。                          |
| ...  | pan               | `A->A       ` | 具有系数（平移）的混音通道。                           |
| ...  | replaygain        | `A->A       ` | ReplayGain扫描仪                            |
| ...  | sidechaincompress | `AA->A      ` | 侧链压缩机                                    |
| ...  | sidechaingate     | `AA->A      ` | 音频侧链门                                    |
| ...  | silencedetect     | `A->A       ` | 检测沉默。                                    |
| ...  | silenceremove     | `A->A       ` | 清除沉默                                     |
| ...  | stereotools       | `A->A       ` | 应用各种立体声工具。                               |
| ...  | stereowiden       | `A->A       ` | 应用立体声加宽效果。                               |
| ...  | treble            | `A->A       ` | 提升或切断较高频率。                               |
| ...  | tremolo           | `A->A       ` | 应用颤音效果。                                  |
| ...  | vibrato           | `A->A       ` | 应用颤音效果。                                  |
| T.C  | volume            | `A->A       ` | 更改输入音量                                   |
| ...  | volumedetect      | `A->A       ` | 检测音量。                                    |
| ...  | aevalsrc          | `|->A       ` | 生成表达式生成的音频信号。                            |
| ...  | anoisesrc         | `|->A       ` | 产生噪声音频信号。                                |
| ...  | anullsrc          | `|->A       ` | 空音频源，返回空音频帧。                             |
| ...  | sine              | `|->A       ` | 生成正弦波音频信号。                               |
| ...  | anullsink         | `A->|       ` | 绝对没有输入音频。                                |
| ...  | alphaextract      | `V->N       ` | 提取Alpha通道作为灰度图像组件。                       |
| ...  | alphamerge        | `VV->V      ` | 将第二个输入的亮度值复制到第一个输入的alpha通道。              |
| ...  | ass               | `V->V       ` | 使用libass库将ASS字幕渲染到输入视频上。                 |
| TS.  | atadenoise        | `V->V       ` | 应用自适应时间平均去噪器。                            |
| TS.  | avgblur           | `V->V       ` | 应用平均模糊滤镜                                 |
| T..  | bbox              | `V->V       ` | 计算每个框架的边界框。                              |
| ...  | bench             | `V->V       ` | 过滤器的基准部分。                                |
| T..  | bitplanenoise     | `V->V       ` | 测量位平面噪声。                                 |
| ...  | blackdetect       | `V->V       ` | 检测（几乎）黑色的视频间隔。                           |
| ...  | blackframe        | `V->V       ` | 检测（几乎）黑色的帧。                              |
| TS.  | blend             | `VV->V      ` | 将两个视频帧混合在一起。                             |
| T..  | boxblur           | `V->V       ` | 模糊输入。                                    |
| TS.  | bwdif             | `V->V       ` | 去输入图像。                                   |
| TS.  | chromakey         | `V->V       ` | 将某种颜色变成透明度。操作YUV颜色。                      |
| ...  | ciescope          | `V->V       ` | 视频CIE范围。                                 |
| T..  | codecview         | `V->V       ` | 可视化有关某些编解码器的信息。                          |
| T..  | colorbalance      | `V->V       ` | 调整色彩平衡。                                  |
| T..  | colorchannelmixer | `V->V       ` | 通过混合颜色通道调整颜色。                            |
| TS.  | colorkey          | `V->V       ` | 将某种颜色变成透明度。操作RGB颜色。                      |
| T..  | colorlevels       | `V->V       ` | 调整颜色级别。                                  |
| TS.  | colormatrix       | `V->V       ` | 转换颜色矩阵。                                  |
| TS.  | colorspace        | `V->V       ` | 转换颜色空间。                                  |
| TS.  | convolution       | `V->V       ` | 应用卷积滤波器                                  |
| ...  | copy              | `V->V       ` | 将输入视频不变地复制到输出。                           |
| ...  | cover_rect        | `V->V       ` | 找到并覆盖用户指定的对象。                            |
| ..C  | crop              | `V->V       ` | 裁剪输入视频。                                  |
| T..  | cropdetect        | `V->V       ` | 自动检测裁剪尺寸。                                |
| TS.  | curves            | `V->V       ` | 调整组件曲线。                                  |
| .S.  | datascope         | `V->V       ` | 视频数据分析。                                  |
| TS.  | dctdnoiz          | `V->V       ` | 使用2D DCT去噪帧。                             |
| TS.  | deband            | `V->V       ` | Debands视频                                |
| ...  | decimate          | `N->V       ` | 抽取帧（后场匹配滤镜）。                             |
| T..  | deflate           | `V->V       ` | 应用放气效果。                                  |
| ...  | deinterlace_qsv   | `V->V       ` | QuickSync视频去隔行扫描                         |
| ...  | dejudder          | `V->V       ` | 去除由拉面产生的抖动。                              |
| T..  | delogo            | `V->V       ` | 从输入视频中删除标志。                              |
| ...  | deshake           | `V->V       ` | 稳定摇摇欲坠的视频。                               |
| ...  | detelecine        | `V->V       ` | 应用反向电视电影模式。                              |
| T..  | dilation          | `V->V       ` | 应用扩张效果。                                  |
| T..  | displace          | `VVV->V     ` | 放置像素                                     |
| T..  | drawbox           | `V->V       ` | 在输入视频画一个彩色的盒子。                           |
| ...  | drawgraph         | `V->V       ` | 使用输入视频元数据绘制图形。                           |
| T..  | drawgrid          | `V->V       ` | 在输入视频上绘制一个彩色网格。                          |
| T.C  | drawtext          | `V->V       ` | 使用libfreetype库在视频帧顶部绘制文本。                |
| T..  | edgedetect        | `V->V       ` | 检测和绘制边缘。                                 |
| ...  | elbg              | `V->V       ` | 使用ELBG算法应用海报效应。                          |
| T.C  | eq                | `V->V       ` | 调整亮度，对比度，伽玛和饱和度。                         |
| T..  | erosion           | `V->V       ` | 施用侵蚀作用。                                  |
| ...  | extractplanes     | `V->N       ` | 将平面提取为灰度帧。                               |
| .S.  | fade              | `V->V       ` | 淡入/淡出输入视频。                               |
| ...  | fftfilt           | `V->V       ` | 对频域中的像素应用任意表达式。                          |
| ...  | field             | `V->V       ` | 从输入视频中提取字段。                              |
| ...  | fieldhint         | `V->V       ` | 使用提示的字段匹配。                               |
| ...  | fieldmatch        | `N->V       ` | 反向电视电影的场匹配。                              |
| T..  | fieldorder        | `V->V       ` | 设置字段顺序。                                  |
| ...  | find_rect         | `V->V       ` | 查找用户指定的对象。                               |
| ...  | format            | `V->V       ` | 将输入视频转换为指定像素格式之一。                        |
| ...  | fps               | `V->V       ` | 强制恒定帧率。                                  |
| ...  | framepack         | `VV->V      ` | 生成一个框架的立体视频。                             |
| ...  | framerate         | `V->V       ` | 在指定的帧速率之间进行采样或缩减采样逐行信号源。                 |
| T..  | framestep         | `V->V       ` | 每N帧选择一帧。                                 |
| ...  | frei0r            | `V->V       ` | 应用frei0r效果。                              |
| T..  | fspp              | `V->V       ` | 应用快速简单的后处理过滤器。                           |
| TS.  | gblur             | `V->V       ` | 应用高斯模糊滤镜                                 |
| T..  | geq               | `V->V       ` | 对每个像素应用一般方程。                             |
| T..  | gradfun           | `V->V       ` | Debands使用渐变快速录像。                         |
| TS.  | haldclut          | `VV->V      ` | 使用Hald CLUT调整颜色。                         |
| TS.  | hflip             | `V->V       ` | 水平翻转输入视频。                                |
| T..  | histeq            | `V->V       ` | 应用全局颜色直方图均衡。                             |
| ...  | histogram         | `V->V       ` | 计算并绘制直方图。                                |
| T..  | hqdn3d            | `V->V       ` | 应用高品质3D降噪器。                              |
| .S.  | hqx               | `V->V       ` | 使用hq * x放大算法将输入缩放2,3或4。                  |
| ...  | hstack            | `N->V       ` | 水平叠加视频输入。                                |
| T.C  | hue               | `V->V       ` | 调整输入视频的色调和饱和度。                           |
| ...  | hwdownload        | `V->V       ` | 将硬件框架下载到正常框架                             |
| ...  | hwupload          | `V->V       ` | 将正常帧上传到硬件框架                              |
| ...  | hwupload_cuda     | `V->V       ` | 将系统内存框上传到CUDA设备。                         |
| T..  | hysteresis        | `VV->V      ` | 通过连接组件将第一个流生成第二个流。                       |
| ...  | idet              | `V->V       ` | 隔行扫描滤波器                                  |
| T..  | il                | `V->V       ` | 去交错或交错字段。                                |
| T..  | inflate           | `V->V       ` | 应用膨胀效果。                                  |
| ...  | interlace         | `V->V       ` | 将逐行视频转换成隔行扫描。                            |
| ...  | interleave        | `N->V       ` | 短时交错视频输入。                                |
| ...  | kerndeint         | `V->V       ` | 应用内核去隔行输入。                               |
| .S.  | lenscorrection    | `V->V       ` | 纠正镜头畸变来纠正图像。                             |
| ...  | loop              | `V->V       ` | 循环视频帧。                                   |
| T..  | lut               | `V->V       ` | 计算并将查找表应用于RGB / YUV输入视频。                 |
| T..  | lut2              | `VV->V      ` | 计算并应用两个视频输入的查找表。                         |
| TS.  | lut3d             | `V->V       ` | 使用3D LUT调整颜色。                            |
| T..  | lutrgb            | `V->V       ` | 计算并将查询表应用于RGB输入视频。                       |
| T..  | lutyuv            | `V->V       ` | 计算并将查询表应用于YUV输入视频。                       |
| T..  | maskedclamp       | `VVV->V     ` | 用第二个流和第三个流夹住第一个流。                        |
| T..  | maskedmerge       | `VVV->V     ` | 使用第三个流作为掩码将第一个流合并。                       |
| ...  | mcdeint           | `V->V       ` | 应用运动补偿去隔行扫描。                             |
| ...  | mergeplanes       | `N->V       ` | 合并飞机                                     |
| ...  | mestimate         | `V->V       ` | 生成运动矢量。                                  |
| T..  | metadata          | `V->V       ` | 操纵视频帧元数据。                                |
| T..  | midequalizer      | `VV->V      ` | 应用中途均衡。                                  |
| ...  | minterpolate      | `V->V       ` | 使用运动插值进行帧速率转换。                           |
| ...  | mpdecimate        | `V->V       ` | 删除近似重复的帧。                                |
| T..  | negate            | `V->V       ` | 否定输入视频。                                  |
| TS.  | nlmeans           | `V->V       ` | 非本地的意思是去噪。                               |
| T..  | nnedi             | `V->V       ` | 应用神经网络边缘定向插值内部去隔行扫描。                     |
| ...  | noformat          | `V->V       ` | 强制libavfilter不使用任何指定的像素格式输入到下一个过滤器。      |
| TS.  | noise             | `V->V       ` | 增加噪音                                     |
| ...  | null              | `V->V       ` | 将源传递给输出。                                 |
| T.C  | overlay           | `VV->V      ` | 在输入的顶部覆盖视频源。                             |
| T..  | owdenoise         | `V->V       ` | 使用小波去噪。                                  |
| ...  | pad               | `V->V       ` | 填写输入视频。                                  |
| ...  | palettegen        | `V->V       ` | 找到给定流的最佳调色板。                             |
| ...  | paletteuse        | `VV->V      ` | 使用调色板来降低输入视频流的采样率。                       |
| ...  | perms             | `V->V       ` | 设置输出视频帧的权限。                              |
| TS.  | perspective       | `V->V       ` | 更正视频的视角。                                 |
| T..  | phase             | `V->V       ` | 相移字段。                                    |
| ...  | pixdesctest       | `V->V       ` | 测试像素格式定义。                                |
| T.C  | pp                | `V->V       ` | 使用libpostproc过滤视频。                       |
| T..  | pp7               | `V->V       ` | 应用后处理7过滤器。                               |
| T..  | premultiply       | `VV->V      ` | 预先第一流与第一流的第二流。                           |
| TS.  | prewitt           | `V->V       ` | 应用prewitt运算符。                            |
| ...  | psnr              | `VV->V      ` | 计算两个视频流之间的PSNR。                          |
| ...  | pullup            | `V->V       ` | 从字段序列上拉到帧。                               |
| T..  | qp                | `V->V       ` | 更改视频量化参数。                                |
| ...  | random            | `V->V       ` | 返回随机帧。                                   |
| T..  | readeia608        | `V->V       ` | 从输入视频中读取EIA-608隐藏式字幕代码，并将其写入帧元数据。        |
| ...  | readvitc          | `V->V       ` | 读取垂直间隔时间码并将其写入帧元数据。                      |
| ...  | realtime          | `V->V       ` | 减慢过滤以实时匹配。                               |
| T..  | remap             | `VVV->V     ` | 重映射像素。                                   |
| TS.  | removegrain       | `V->V       ` | 去除谷物。                                    |
| T..  | removelogo        | `V->V       ` | 根据掩模图像删除电视标志。                            |
| ...  | repeatfields      | `V->V       ` | 基于MPEG重复字段标志的硬重复字段。                      |
| ...  | reverse           | `V->V       ` | 反转剪辑                                     |
| TSC  | rotate            | `V->V       ` | 旋转输入图像。                                  |
| T..  | sab               | `V->V       ` | 应用形状自适应模糊。                               |
| ..C  | scale             | `V->V       ` | 缩放输入视频大小和/或转换图像格式。                       |
| ...  | scale_qsv         | `V->V       ` | QuickSync视频缩放和格式转换                       |
| ..C  | scale2ref         | `VV->VV     ` | 缩放输入视频大小和/或将图像格式转换为给定的参考。                |
| ...  | select            | `V->N       ` | 选择视频帧传递输出。                               |
| TS.  | selectivecolor    | `V->V       ` | 对特定颜色范围应用CMYK调整。                         |
| ...  | sendcmd           | `V->V       ` | 发送命令到过滤器。                                |
| ...  | separatefields    | `V->V       ` | 将输入视频帧分割成字段。                             |
| ...  | setdar            | `V->V       ` | 设置帧显示宽高比。                                |
| ...  | setfield          | `V->V       ` | 输出视频帧的强制字段。                              |
| ...  | setpts            | `V->V       ` | 设置输出视频帧的PTS。                             |
| ...  | setsar            | `V->V       ` | 设置像素样本宽高比。                               |
| ...  | settb             | `V->V       ` | 设置视频输出链接的时基。                             |
| ...  | showinfo          | `V->V       ` | 显示每个视频帧的文字信息。                            |
| T..  | showpalette       | `V->V       ` | 显示框架调色板。                                 |
| T..  | shuffleframes     | `V->V       ` | 随机播放视频帧。                                 |
| ...  | shuffleplanes     | `V->V       ` | 随机播放视频飞机                                 |
| T..  | sidedata          | `V->V       ` | 操纵视频帧端数据。                                |
| .S.  | signalstats       | `V->V       ` | 从视频分析生成统计信息。                             |
| T..  | smartblur         | `V->V       ` | 模糊输入视频，而不影响轮廓。                           |
| TS.  | sobel             | `V->V       ` | 应用sobel操作员                               |
| ...  | split             | `V->N       ` | 将输入传递到N个视频输出。                            |
| T.C  | spp               | `V->V       ` | 应用简单的后期处理过滤器。                            |
| ...  | ssim              | `VV->V      ` | 计算两个视频流之间的SSIM。                          |
| .S.  | stereo3d          | `V->V       ` | 转换视频立体3D视图。                              |
| ..C  | streamselect      | `N->N       ` | 选择视频流                                    |
| ...  | subtitles         | `V->V       ` | 使用libass库将文本字幕渲染到输入视频上。                  |
| ...  | super2xsai        | `V->V       ` | 使用Super2xSaI像素艺术算法将输入缩放2倍。               |
| T..  | swaprect          | `V->V       ` | 在视频中交换2个矩形对象。                            |
| T..  | swapuv            | `V->V       ` | 交换U和V组件。                                 |
| .S.  | tblend            | `V->V       ` | 混合连续帧。                                   |
| ...  | telecine          | `V->V       ` | 应用电视电影模式。                                |
| T..  | threshold         | `VVVV->V    ` | 使用其他视频流的阈值第一视频流。                         |
| ...  | thumbnail         | `V->V       ` | 在给定的连续帧序列中选择最具代表性的帧。                     |
| ...  | tile              | `V->V       ` | 将几个连续的帧平铺在一起。                            |
| ...  | tinterlace        | `V->V       ` | 执行时间字段隔行扫描。                              |
| .S.  | transpose         | `V->V       ` | 调换输入视频。                                  |
| ...  | trim              | `V->V       ` | 从输入中选择一个连续的部分，放下其余部分。                    |
| T..  | unsharp           | `V->V       ` | 锐化或模糊输入视频。                               |
| T..  | uspp              | `V->V       ` | 应用超简单/慢速后处理过滤器。                          |
| T..  | vaguedenoiser     | `V->V       ` | 应用基于小波的去噪器。                              |
| ...  | vectorscope       | `V->V       ` | 视频矢量图                                    |
| T..  | vflip             | `V->V       ` | 垂直翻转输入视频。                                |
| ...  | vidstabdetect     | `V->V       ` | 提取相对转换，通过1的2进行稳定（参见vidstabtransform for pass 2）。 |
| ...  | vidstabtransform  | `V->V       ` | 转换帧，通过2的2进行稳定（参见vidstabdetect通过1）。       |
| T..  | vignette          | `V->V       ` | 制作或倒转小插曲效果。                              |
| ...  | vstack            | `N->V       ` | 垂直堆叠视频输入。                                |
| TS.  | w3fdif            | `V->V       ` | 应用马丁·韦斯顿三场去隔行。                           |
| ...  | waveform          | `V->V       ` | 视频波形监视器。                                 |
| ...  | weave             | `V->V       ` | 将输入视频字段编织成帧。                             |
| .S.  | xbr               | `V->V       ` | 使用xBR算法缩放输入。                             |
| TS.  | yadif             | `V->V       ` | 去输入图像。                                   |
| T..  | zoompan           | `V->V       ` | 应用缩放和平移效果。                               |
| ..C  | zscale            | `V->V       ` | 应用调整大小，颜色空间和位深度转换。                       |
| ...  | allrgb            | `|->V       ` | 生成所有RGB颜色。                               |
| ...  | allyuv            | `|->V       ` | 生成所有的yuv颜色。                              |
| ...  | cellauto          | `|->V       ` | 创建由基本单元自动机生成的模式。                         |
| ..C  | color             | `|->V       ` | 提供均匀的彩色输入。                               |
| ...  | frei0r_src        | `|->V       ` | 生成一个frei0r源。                             |
| ...  | haldclutsrc       | `|->V       ` | 提供身份Hald CLUT。                           |
| ...  | life              | `|->V       ` | 创造生活                                     |
| ...  | mandelbrot        | `|->V       ` | 渲染Mandelbrot分形。                          |
| ...  | mptestsrc         | `|->V       ` | 生成各种测试图案。                                |
| ...  | nullsrc           | `|->V       ` | 空视频源，返回未处理的视频帧。                          |
| ...  | rgbtestsrc        | `|->V       ` | 生成RGB测试图案。                               |
| ...  | smptebars         | `|->V       ` | 生成SMPTE彩条。                               |
| ...  | smptehdbars       | `|->V       ` | 生成SMPTE高清彩条。                             |
| ...  | testsrc           | `|->V       ` | 生成测试图案。                                  |
| ...  | testsrc2          | `|->V       ` | 生成另一个测试模式。                               |
| ...  | yuvtestsrc        | `|->V       ` | 生成YUV测试图案。                               |
| ...  | nullsink          | `V->|       ` | 对输入视频绝对没有任何东西。                           |
| ...  | abitscope         | `A->V       ` | 将输入音频转换为音频位视频输出。                         |
| ...  | adrawgraph        | `A->V       ` | 使用输入音频元数据绘制图形。                           |
| ...  | ahistogram        | `A->V       ` | 将输入音频转换为直方图视频输出。                         |
| ...  | aphasemeter       | `A->N       ` | 将输入音频转换为相位计视频输出。                         |
| ...  | avectorscope      | `A->V       ` | 将输入音频转换为vectorcope视频输出。                  |
| ...  | concat            | `N->N       ` | 连接音视频流。                                  |
| ...  | showcqt           | `A->V       ` | 将输入音频转换为CQT（恒定/钳位Q变换）频谱视频输出。             |
| ...  | showfreqs         | `A->V       ` | 将输入音频转换为频率视频输出。                          |
| .S.  | showspectrum      | `A->V       ` | 将输入音频转换为频谱视频输出。                          |
| .S.  | showspectrumpic   | `A->V       ` | 将输入音频转换为频谱视频输出单张图像。                      |
| ...  | showvolume        | `A->V       ` | 将输入音频转换为视频输出。                            |
| ...  | showwaves         | `A->V       ` | 将输入音频转换为视频输出。                            |
| ...  | showwavespic      | `A->V       ` | 将输入音频转换为视频输出单张图像。                        |
| ...  | spectrumsynth     | `VV->A      ` | 将输入频谱视频转换为音频输出。                          |
| ..C  | amovie            | `|->N       ` | 从电影来源读取音频。                               |
| ..C  | movie             | `|->N       ` | 从电影来源阅读。                                 |
| ...  | abuffer           | `|->A       ` | 缓冲音频帧，使它们可以访问过滤器链。                       |
| ...  | buffer            | `|->V       ` | 缓冲视频帧，使其可以访问过滤器链。                        |
| ...  | abuffersink       | `A->|       ` | 缓冲音频帧，并将其提供给过滤器图形的末尾。                    |
| ...  | buffersink        | `V->|       ` | 缓冲视频帧，并使它们可用于过滤器图形的末尾。                   |
| ...  | afifo             | `A->A       ` | 缓冲区输入框，并在请求时发送它们。                        |
| ...  | fifo              | `V->V       ` | 缓冲输入图像并在请求时发送它们。                         |