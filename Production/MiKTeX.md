# MikTex

## 修复中文输出



```Tex
\usepackage[UTF8]{ctex}
\usepackage{graphicx}
\usepackage[T1]{fontenc}
\usepackage{mathpazo}
\usepackage[warn]{textcomp}
```
进package manager重装fontspec换XeLaTex

```Tex
\usepackage{xeCJK}
\setCJKmainfont{simsun.ttc}
\setCJKsansfont{simhei.ttf}
\setCJKmonofont{simfang.ttf}
```

