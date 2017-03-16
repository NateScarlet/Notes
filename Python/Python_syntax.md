[TOC]

# 语法

## 简单语句

### 表达式Expression

### 赋值 Assignment

```python
变量 = 变量值
```

多重赋值

```python
a, b = 0, 1
```

### 断言Assert

### 计算

| 符号   | 说明                |
| ---- | ----------------- |
| //   | floor除法           |
| %    | 取余                |
| **   | 乘方                |
| _    | 最近一个表达式的值(仅限交互模式) |

### 比较

和别的语言一样

### 转义

\

### 序列拆封

变量1, 变量2, 变量3, ..., 变量n = n个元素的序列

### 语句列表

| 语句         | 说明      |
| ---------- | ------- |
| pass       | 跳过      |
| del        | 删除      |
| return     | 返回      |
| yield      |         |
| raise      |         |
| break      | 中断      |
| continue   | 继续      |
| import     | 导入      |
| global 变量名 | 声明全局变量  |
| nonlocal   | 声明非局部变量 |



## 复合语句

### 如果 if

```python
if 判断语句:
    执行语句
elif 判断语句:
    执行语句
elif 判断语句:
    执行语句
else:
    执行语句
```

### 当 while

```python
while 条件语句:
	条件语句为真时的执行语句
```



#### else

它在循环迭代完整个列表（对于 for ）或执行条件为 false （对于 while ）时执行

### 为 for

```python
for 向后引用的变量名 in 序列:
    执行语句
```

序列加"[:]" 来迭代序列的副本

### 异常处理 try except 

```python
try:
    执行语句
except 异常名(为空代表所有异常):
    执行语句
```

### with

### 函数定义

```python
def 函数名([参数=参数默认值, 参数, ...]):
    执行语句
```

调用时使用

```python
函数名(位置参数1)
函数名(关键字参数名1=值)
函数名(关键字参数名1=值, 关键字参数名2=值)
```

### 类定义 Class definitions

## 类型
* 字符串

  * ‘字符串’ 在字符串内有单引号没有双引号时使用 "字符串"

    使用\转义单引号

  * r'字符串'
    防止\被当作特殊字符标志

  * u'字符串'
    unicode字符串

  * """字符串""" 或者 '''字符串'''
    换行(包含不可见换行符)

    \放在行尾(即不可见换行符之前)可以避免换行

  * 操作符

    * '字符串' + '字符串'
      连接
    * ‘字符串’‘字符串’
      相邻字符串自动连接(不支持变量和表达式)
    * 整数 * '字符串'
      重复

  * '字符串'[整数]
    索引

    有个办法可以很容易地记住切片的工作方式：切片时的索引是在两个字符 之间 。左边第一个字符的索引为 0，而长度为 n 的字符串其最后一个字符的右界索引为 n。

     +---+---+---+---+---+---+
     | P | y | t | h | o | n |
     +---+---+---+---+---+---+
     0   1   2   3   4   5   6
    -6  -5  -4  -3  -2  -1

    * 负数索引

      从右计算

  * '字符串'[整数:整数]
    切片

    * 第一个整数默认为0,第二个整数默认为字符串大小

      ```python
      >>> word[:2]  # character from the beginning to position 2 (excluded)
      'Py'
      >>> word[4:]  # characters from position 4 (included) to the end
      'on'
      >>> word[-2:] # characters from the second-last (included) to the end
      'on'
      ```

    * 过大值会被字符串实际长度代替

    * 第一个整数比第二个整数大时返回空字符串


* 列表

  列表[索引号]

* 数值

  * 整数int
  * 浮点数float
  * complex

### 

# Python优化建议

[Python Enhancement Proposals(PEPs)](https://www.python.org/dev/peps/)