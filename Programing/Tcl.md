[TOC]
# 概念
* 所有东西都是字符串
* 词语word
* 命令command
* 参数
* 事件Events
* 子进程调用subprocess invocation
* 阵列Array
* 列表List

#语法
* 空格分割词语

* 命令 参数1 参数2 ...

* 分号或者换行来分行

* $前缀表示此词语是变量

* 嵌套

  `命令1 [命令2]`
  将命令2的结果作为命令1的参数

* “引用”

  变量将被应用

  输出不包含引号

## 控制结构

### 循环

```Tcl
while ｛判断语句｝｛
    Tcl脚本
｝
```
```Tcl
if {条件} {
    表达式1
} else {
    表达式2
}
```
`for`
`foreach`
`switch`

### 判断
还是那套符号

### 声明过程
```Tcl
proc 过程名 {参数名1 参数名2 ...}{
    Tcl脚本
}
```

#自带变量

| 变量名         | 含义    |
| ----------- | ----- |
| tcl_version | Tcl版本 |

#内置命令
`?参数? `
表示可选参数

| 命令                                       | 说明              |
| ---------------------------------------- | --------------- |
| after                                    |                 |
| append                                   |                 |
| apply                                    |                 |
| argc                                     |                 |
| argv                                     |                 |
| expr 表达式内容                               | 表达式             |
| set 变量名 变量值                              | 设置变量            |
| return 返回值                               | 返回值             |
| lrange 列表 起始索引 结束索引                      | 切片              |
| lsort ?选项? 列表                            | 排序              |
| for 起始状态 测真 下一个 主体                       |                 |
| put  ?-nonewline? ?频道id? 字符串             |                 |
| split 字符串 ?指定分割符集?                       | 分割 默认分隔符为空格     |
| subst ?-nobackslashes? ?-nocommands? ?-novariables? 字符串 | 代入字符串中的转义、命令、变量 |
| proc                                     | 声明过程            |
| regsub                                   |                 |
| regexp                                   |                 |
## file
| 命令             | 说明   |
| -------------- | ---- |
| file tail      |      |
| file rootname  |      |
| file dirname   |      |
| file extension |      |
| file mkdir     |      |
| file copy      |      |
| file delete    |      |

## string

| 命令                                       | 说明          |
| ---------------------------------------- | ----------- |
| string is 类型 ?-strict?  ?-failindex 变量名? 内容 | 返回内容是否为指定类型 |
| length                                   |             |
| map                                      |             |
| equal                                    |             |

类型:

* integer
  32位以内的整数
* entier
  任何大小的整数
* digit
  只包含数字的字符串