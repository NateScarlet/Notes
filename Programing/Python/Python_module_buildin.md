[TOC]

# 内置模块 build-in module

## 函数

- `help([对象])`

  **调用帮助**

  Invoke the built-in help system. (This function is intended for interactive use.) If no argument is given, the interactive help system starts on the interpreter console. If the argument is a string, then the string is looked up as the name of a module, function, class, method, keyword, or documentation topic, and a help page is printed on the console. If the argument is any other kind of object, a help page on the object is generated.

  This function is added to the built-in namespace by the site module.

  Changed in version 3.4: Changes to pydoc and inspect mean that the reported signatures for callables are now more comprehensive and consistent.

- `print()`

- `write()`

- `len()`

  返回对象长度

- `abs(x)`

  返回数字的绝对值

  Return the absolute value of a number. The argument may be an integer or a floating point number. If the argument is a complex number, its magnitude is returned.

- `all(可迭代)`

  返回是否所有元素为真

  Return True if all elements of the iterable are true (or if the iterable is empty). Equivalent to:

  ​

  ```python
  def all(iterable):
      for element in iterable:
          if not element:
              return False
      return True
  ```


- `any(可迭代)`

  返回是否任意元素为真

  ```python
  def any(iterable):
      for element in iterable:
          if element:
              return True
      return False
  ```



- `ascii(对象)`

  As repr(), return a string containing a printable representation of an object, but escape the non-ASCII characters in the string returned by repr() using \x, \u or \U escapes. This generates a string similar to that returned by repr() in Python 2.

- `bin(x)`

- 整数转二进制

  Convert an integer number to a binary string. The result is a valid Python expression. If x is not a Python int object, it has to define an **index**() method that returns an integer.

- `类 bool([x])`布尔运算

  Return a Boolean value, i.e. one of True or False. x is converted using the standard truth testing procedure. If x is false or omitted, this returns False; otherwise it returns True. The bool class is a subclass of int (see Numeric Types — int, float, complex). It cannot be subclassed further. Its only instances are False and True (see Boolean Values).

- `类 bytearray([源[, 解码[. 错误]]])`

  Return a new array of bytes. The bytearray class is a mutable sequence of integers in the range 0 <= x < 256. It has most of the usual methods of mutable sequences, described in Mutable Sequence Types, as well as most methods that the bytes type has, see Bytes and Bytearray Operations.

  The optional source parameter can be used to initialize the array in a few different ways:

  If it is a string, you must also give the encoding (and optionally, errors) parameters; bytearray() then converts the string to bytes using str.encode().If it is an integer, the array will have that size and will be initialized with null bytes.If it is an object conforming to the buffer interface, a read-only buffer of the object will be used to initialize the bytes array.If it is an iterable, it must be an iterable of integers in the range 0 <= x < 256, which are used as the initial contents of the array.Without an argument, an array of size 0 is created.

  See also Binary Sequence Types — bytes, bytearray, memoryview and Bytearray Objects.

- `类 bytes(源[, 解码[. 错误]]])`

- `callable(对象)`是否可调用

- `chr(索引)`返回索引对应的字符

- `delattr(对象, 属性名)`删除指定对象的指定属性

  This is a relative of setattr(). The arguments are an object and a string. The string must be the name of one of the object’s attributes. The function deletes the named attribute, provided the object allows it. For example, delattr(x, 'foobar') is equivalent to del x.foobar.

  class dict(**kwarg)class dict(mapping, **kwarg)class dict(iterable, **kwarg)Create a new dictionary. The dict object is the dictionary class. See dict and Mapping Types — dict for documentation about this class.

  For other containers see the built-in list, set, and tuple classes, as well as the collections module.

- `dir([对象])`返回局部名称/对象属性列表

- `divmod(a, b)`返回(a/b向下取整, a/b的余数)

  Take two (non complex) numbers as arguments and return a pair of numbers consisting of their quotient and remainder when using integer division. With mixed operand types, the rules for binary arithmetic operators apply. For integers, the result is the same as (a // b, a % b). For floating point numbers the result is (q, a % b), where q is usually math.floor(a / b) but may be 1 less than that. In any case q * b + a % b is very close to a, if a % b is non-zero it has the same sign as b, and 0 <= abs(a % b) < abs(b).

- `eval(表达式,globals=None,locals=None)`

  把字符串当成命令执行

  The arguments are a string and optional globals and locals. If provided, globals must be a dictionary. If provided, locals can be any mapping object.

  The expression argument is parsed and evaluated as a Python expression (technically speaking, a condition list) using the globals and locals dictionaries as global and local namespace. If the globals dictionary is present and lacks ‘`__builtins__`’, the current globals are copied into globals before expression is parsed. This means that expression normally has full access to the standard builtins module and restricted environments are propagated. If the locals dictionary is omitted it defaults to the globals dictionary. If both dictionaries are omitted, the expression is executed in the environment where eval() is called. The return value is the result of the evaluated expression. Syntax errors are reported as exceptions. Example:

  ```python
  >>>
  >>> x = 1
  >>> eval('x+1')
  2
  ```

    This function can also be used to execute arbitrary code objects (such as those created by compile()). In this case pass a code object instead of a string. If the code object has been compiled with 'exec' as the mode argument, eval()‘s return value will be None.

  Hints: dynamic execution of statements is supported by the exec() function. The globals() and locals() functions returns the current global and local dictionary, respectively, which may be useful to pass around for use by eval() or exec().

  See `ast.literal_eval()` for a function that can safely evaluate strings with expressions containing only literals.


- `ord(字符)`

  返回字符对应的索引

- `str()`返回于人阅读的字符串

- `类 list([可迭代])`

- `range(停止)`range(开始, 停止[, 步进])迭代范围

- `len(对象, /)`返回对象内含的元素数量

- getattr()

### 常量

| 常量    |      |
| ----- | ---- |
| False |      |
| True  |      |
| None  |      |

### 变量

| 变量         |           |
| ---------- | --------- |
| `__file__` | 脚本文件路径    |
| `__name__` | 当前使用的命名空间 |
|            |           |

# 字符串对象 str object

## 方法

```
capitalize()
首字母大写
casefold()
小写(较激进)
center()
isdigit()
是否为数字
join(列表)
用字符串对列表进行连接
strip([字符])
移除字符串头尾指定的字符（默认为空格）
replace(查找的字符串, 替换的字符串[, 替换次数])
format(*args, **kwargs)
startswith(prefix[, start[, end]])
返回是否有指定前缀
```



# 列表对象list object

## 方法

```
insert(索引号, 字符串)
在指定位置插入
append()
__len__()
返回列表元素个数
pop([索引])
返回索引号代表的字符串(默认为最后一个), 并且将它从列表中移除
sort(key=none, reverse=False)
排序
	key排序关键词
	reverse反转
```





# 字典对象dict object

## 方法

```
fromkeys( 字符串[, 值])
get( 关键字[, 默认值])
获取指定值
keys()
返回关键字列表
pop( 关键字[, 默认值] )
移除指定关键字并返回
values()
返回值列表
clear()
清空
copy()
复制
```

