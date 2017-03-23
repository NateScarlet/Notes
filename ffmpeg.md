# FFMPEG

## 语法

ffmpeg -i 输入的文件 [选项...] 输出的文件名

## 选项

| 选项           | 说明                              |
| ------------ | ------------------------------- |
| -an          | 去除声音                            |
| -vn          | 去除                              |
| -vf  "滤镜"    | 视频滤镜                            |
| -vcodec 视频编码 | 指定视频编码                          |
| -acodec 音频编码 | 指定音频编码                          |
| -preset 编码预设 | 指定编码预设                          |
| -crf 质量系数    | 指定0到51的crf(ConstrantRateFactor) |

## -vf

`scale=1920:1080`

```
scale=trunc(iw/2)*2:trunc(ih/2)*2
```

## 视频/音频编码

`copy`使用原本的编码

视频编码

* libx264

音频编码

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