[TOC]

# 概念

* 函数function

  和对象无关

* 方法method

  和对象相关

  * 实例方法
  * 静态方法
  * 类方法

* 实例 Instance

* 模块 module

  在python中一个文件可以被看成一个独立模块

* 包 Package

  而包对应着文件夹

* 类class

  * 子类subclass
  * 超类superclass

* 序列类型sequence type
  * 链表

  * 字符串string

    空字符串‘’

  * 元组tuple

    一个元组由数个逗号分隔的值组成
    不可变

    空元组()

  * 列表list

    空列表[]

* 映射mapping

* 迭代

  * 迭代器
    for
    list()
  * 可迭代
    range()

* 回调Callback

* 调用invoke

* 提示符prompt

* 进制开头

  * 二进制0b
  * 八进制0
  * 十六进制0x


## 测真流程truth testing procedure

### 为假

* None

* Flase

* 任何数值型的0

* 任何空序列比如：'',(),[]

* 任何空映射比如：｛｝

* 未定义类的实例

### 为真

* 任何不为假的值

##  词汇分析Lexical Analysis

Python 程序由 parser 解析器 读取。 语法分析器的输入是 tokens 标记 的流, 此流是 lexical analyzer 词汇分析器 生成的。

Python 将程序文本作为 Unicode 代码点读取;源文件编码时能够被设置一个编码声明,默认是 UTF-8, 详情参见 PEP 3210. 如果原文件不能被解码, 将会出现 SyntaxError 语法错误 。

### 行结构Line structure

Python 程序被分割成一定数量的 logical lines 逻辑行。

#### 逻辑行Logical lines

一个逻辑行的结束用 标志 NEWLINE 表示。 语句不穿过逻辑行边界除非语法允许 NEWLINE (例如, 在 compound复合 语句 的语句之间)。 一个逻辑行是由单个或多个 physical lines 物理行 依据显式或隐式 line joining 行连接 规则构造的。

#### 物理行Physical lines

物理行是以行序列结束的字符序列。 在源文件中, 任何的标准平台行结束序列都能使用 - Unix  格式使用 ASCII LF(linefeed 换行), Windows 格式 使用 ASCII 序列 CR LF(回车后跟换行), 或者 老 Macintosh 格式 使用 CR(回车) 字符。 所有这些形式都能平等的使用, 无论在何平台。

在内置 Python 中, 源代码字符串应该通过 Python API 使用标准 C 常规新行字符 (\n 字符 表示 ASCII LF ,作为换行符)。

#### 注释Comments

注释用井号字符(#)起始,井号字符不参与迭代, 并且以物理行结束。 一个注释标志了一个逻辑行的结束 除非有隐式世行连接归结介入。注释被语法无视;它们没有标志(tokens)。

#### 编码声明Encoding declarations
如果 Python 脚本的第一或者第二行吻合标准表达式 coding[=:]\s*([-\w.]+) , 此注释将被作为编码生命执行; 这个表达式的第一组吻合命名源代码文件的编码。 编码声明必定是单独一行。 如果在第二行, 则第一行必须也是 仅有注释的行。 推荐的编码表达式格式为
`# -*- coding: <encoding-name> -*-`
此格式能被 GNU Emacs 文本编辑器识别,及
`# vim:fileencoding=<encoding-name>`
此格式能被 Bram Moolenaar’s VIM 文本编辑器识别。

如果没有找到编码声明,默认编码为 UTF-8。 并且, 如果文件的第一个字节为 UTF-8 字节序标记(b’\xef\xbb\xbf’),声明过的文件编码为 UTF-8 (被微软记事本及其他的的软件支持)。

如果编码被声明, 编码名称必须能被 Python 识别。 编码将被用于所有的语汇分析,包括字符串迭代, 注释 和 标识符。

#### 显示行连接Explicit line joining

两个或者更多物理行可以用反斜杠字符(\)连接成为单个逻辑行,如下所述: 当一个物理行以不是迭代或者注释一部分的反斜杠结束时,它将和后面的内容结合成为单个逻辑行, 删除反斜杠和紧跟的行结束字符。例如:
```python
if 1900 < year < 2100 and 1 <= month <= 12 \
    and 1 <= day <= 31 and 0 <= hour < 24 \
    and 0 <= minute < 60 and 0 <= second < 60: # Looks like a valid date
        return 1
```
用反斜杠结束的行不能附带注释。 反斜杠不会延续注释。 反斜杠除非是用于字符串迭代不会延续标记 (也就是说,除了字符串迭代以外的标记不能被反斜杠分割成不同的物理行)。反斜杠字符串迭代的在其他地方出现是非法的。

#### 隐式行连接Implicit line joining

在小括号,中括号和大括号中的表达式能够被分割成多个物理行而不需要反斜杠。例如:

```python
month_names = ['Januari', 'Februari', 'Maart',    # These are the
               'April', 'Mei', 'Juni',            # Dutch names
               'Juli', 'Augustus', 'September',   # for the months
               'Oktober', 'November', 'December'] # of the year
```

隐式连接能够附带注释。下一行的缩进无关紧要。空行是允许的。 在隐式连接行之间是没有 NEWLINE 标志的。 隐式连接行也能在 三引号内的字符串中发生;这种情况下它们不能附带注释。

#### 空行Blank lines

只含有空格,制表符(Tab),换页(formfeed)或者注释的逻辑行将被无视(换而言之,将不会生成 NEWLINE 标志)。在交互式语句的输入中,空行的处理可能会根据 读取计算输出 循环 的执行而不同。在标准交互式解释器中,完全逻辑空行(连空格和注释都不含有的空行)将结束多行语句。

#### 缩进 Indentation

逻辑行行首的空白(空格和换行符)用于计算此行的缩进等级,缩进等级决定语句的组。

制表符将在逻辑行的开始被一到八个空格替换(从左到右),以使总空格数量成为8的倍数(试图使用和 Unix 相同的方法)。在第一个非空字符前的空格数量决定了此行的错金。缩进不能用反斜杠分割成多个物理行;空格遇到的第一个反斜杠将结束缩进、

如果源文件以混合了制表符和空格。缩进将因不符合被拒绝。

#### 标志间的空白Whitespace between tokens