# Python 教程

## 更精美的输出格式

目前为止我们接触到了两种写入值的方法: _表达式语句_ 和 `print()` 函数。(第三种方法是使用文件对象的`write()`方法; 默认输出文件能够用`sys.stdout`引用。查看库引用获取更多关于此的信息。)

通常你想要更好地控制你的输出,而不仅是简单用空格分割的值。有两种方法来指定你输出的格式; 第一种方法是你手动处理所有的字符串;使用字符串分割和连接操作你可以完全使输出达到你想要的效果。字符类型有许多实用的方法来操作附加的字符串来进行分列。第二种方法是使用`str.format()`方法。

`string`模块包含了一个`Template`类来提供另一种调整字符中的值的方法。

当然还有另一个疑问: 如何将值转换为字符串? 幸运的是, Python有转换任何值为字符串的方法: 将它通过`repr()`或者`str()`函数。

 `str()`函数意图返回人类可读的优雅的值, 当`repr()`意图生成能被解释器识别的的表现(当然, 如果没有相对应的语法会导致`SyntaxError`)。对没有实际人类可读值的每一个对象, `str()`将会返回和`repr()`相同的值。许多种类的值,例如数字或者像是列表和字典的结构, 使用两种函数有相同的表达。 实际上字符串有两种截然不同的表现。

一些例子:

```python
>>> s = 'Hello, world.'
>>> str(s)
'Hello, world.'
>>> repr(s)
"'Hello, world.'"
>>> str(1/7)
'0.14285714285714285'
>>> x = 10 * 3.25
>>> y = 200 * 200
>>> s = 'The value of x is ' + repr(x) + ', and y is ' + repr(y) + '...'
>>> print(s)
The value of x is 32.5, and y is 40000...
>>> # The repr() of a string adds string quotes and backslashes:
... hello = 'hello, world\n'
>>> hellos = repr(hello)
>>> print(hellos)
'hello, world\n'
>>> # The argument to repr() may be any Python object:
... repr((x, y, ('spam', 'eggs')))
"(32.5, 40000, ('spam', 'eggs'))"
```

这里是两种写入平方和立方表的方法:

```python
>>> for x in range(1, 11):
... print(repr(x).rjust(2), repr(x*x).rjust(3), end=' ')
... # Note use of 'end' on previous line
... print(repr(x*x*x).rjust(4))
...
 1   1    1
 2   4    8
 3   9   27
 4  16   64
 5  25  125
 6  36  216
 7  49  343
 8  64  512
 9  81  729
10 100 1000
>>> for x in range(1, 11):
... print('{0:2d} {1:3d} {2:4d}'.format(x, x*x, x*x*x))
...
 1   1    1
 2   4    8
 3   9   27
 4  16   64
 5  25  125
 6  36  216
 7  49  343
 8  64  512
 9  81  729
10 100 1000
```

