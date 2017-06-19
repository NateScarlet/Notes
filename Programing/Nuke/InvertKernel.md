[TOC]

# 内核(Kernel)介绍

我们首先将要认识是一个简单将单个图像作为输入, 反转它的颜色, 然后乘以某个值最后写入输出图像的内核。 

## 反转内核(InvertKernel)

```C++
kernel InvertKernel : ImageComputationKernel<eComponentWise>
{
  Image<eRead, eAccessPoint, eEdgeClamped> src;  //the input image
  Image<eWrite> dst;  //the output image

  param:
    float multiply;  //This parameter is made available to the user.

  local:
    float _whiteAccessPoint;  //This local variable is not exposed to the user.

  //In define(), parameters can be given labels and default values.
  void define() {
    defineParam(multiply, "Multiply", 1.0f);
  }

  //The init() function is run before any calls to process().
  void init() {
    _whiteAccessPoint = 1.0f;  //Local variables can be initialised here.
  }

  //The process function is run at every pixel to produce the output.
  void process() {
    //Invert the input value from src and multiply:
    dst() = (_whiteAccessPoint - src()) * multiply;
   }
};
```

## 内核与迭代

Blink内核以和C++相似的方式声明:

```C++
kernel InvertKernel : ImageComputationKernel<eComponentWise>
```

这一行告诉我们反转内核是一个blink"内核", 和C++的类很相似。这个Blink内核从`ImageComputationKernel`继承, 它是一个用于生成输出图像的内核。 这个内核采用分量形式(componentwise)的行为(`eCompnentWise`)。 分量形式意味着输出图像的每个通道将会被单独处理。 当处理每个通道时, 只有相对应通道的的输入数据能被访问。

一个备选方案是使用像素形式(pixelwise)的内核(`ePixelWise`)。像素形式的内核能在每个像素输出到所有通道并且能访问输入数据的所有通道。你应该为任何涉及多个通道互相影响的操作使用像素形式的内核, 比如饱和度调整。一个像素形式的内核像这样声明:

```C++
kernel SaturationKernel : ImageComputationKernel<ePixelWise>
```

当使用图像处理内核(ImageComputationKernel)时, 你不能控制处理输出像素(对于像素形式内核)或者输出组件(对于分量形式内核)的顺序。 内核调用会对输出空间的每一点都进行。 目的是所有的内核调用都是互相独立并且可同时进行的。 最少在GPU上, 上千的内核调用会同时进行。 我们的反转内核就是个这种方式的例子: 每个输出值都能单独计算, 并不依赖输出的其他值。 事实上, 许多图像处理操作都差不多能直接映射到平行处理模型。



## 图像指定

在内核结构(body)内部我们需要指定它需要的图像。 反转内核有一个输入src和一个输出图像dst, 像这样声明:

```C++
  Image<eRead, eAccessPoint, eEdgeClamped> src;  //the input image
  Image<eWrite> dst;  //the output image
```

这告诉我们src是一个`Image`类对象, 并且`eRead`告诉我们对这个图像仅读取访问。 dst同样是一个`Image`类对象但是我们需要写入访问`eWrite`.

在图像指定时你能告诉编译器更多你想要如何访问图像和当你想访问图像范围外时应该怎么做。例如, 在反转内核中输入图像有`eAccessPoint`访问, 这意味着他只在输出图像的当前位置才会访问。 它还有一个边缘方法`eEdgeClamped`定义了边缘外的像素将会用边缘像素进行重复。我们将在下一节看到更多关于图像指定器的例子。

所有的内核都应该有至少一个输出图像, 你应该用这样的一行来定义:

```C++
Image<eWrite> dst;
```

## 参数

内核的参数将在_param_代码段中定义, 和你在C++类中定义成员变量时一样。 如果你的内核不需要任何参数, 你可以忽略这一代码段。

反转内核只有一个参数_multiply_:

```C++
  param:
    float multiply;  //This parameter is made available to the user.
```

当内核被编译在一个BlinkScript节点内时, 节点将会为内核的每个参数生成一个调整参数(knob), 并且将它添加到**Kernel Parameters**标签页中。 一当创建, 节点将只有一个参数**Multiply**。

内核参数可以是C++内置类型例如float或者int。 还支持向量参数: float2, float3 及 float4, 他们分别代表了2、3、4维向量, 并且类似的还有 int2, int3, int4。同样支持 float3x3(3x3矩阵) 及 float4x4(4x4矩阵) 矩阵类型。

## 局部变量

你能在内核的_local_代码段中添加不显示给用户的局部变量。 当然如果你不想要使用局部参数, 你可以忽略这一代码段。

反转内核只有一个局部变量__whitePoint_。 它用来反转输入的彩色图像的, 并且我们假设输入图像的白点为1.

和参数一样, 局部变量能够是C++内置类型, 例如: float 或者 int; 向量类型 float2, float3, float4, int2, in3 和 int4; 或者矩阵类型 float3x3 or float4x4。

局部变量能在_[init()函数](#init()函数)_中设定, 它在平行处理阶段(_[process()函数](#process()函数)_)之前运行一个单线程。_process()_能够一次性同时运行多个线程, 并且每个_process()_的实例都对局部变量的权限是只读的。 如果你需要, 你可以声明只能在当前线程中读写的临时变量。

## define()函数

可以在define函数中设置参数, 调用difineParam()。 defineParam使用三个参数: 参数名称, 要显示给用户的字符串, 和参数的默认值。 在这里, _multiply_ 参数用**Multiply**显示, 并且默认值为1:

```C++
  void define() {
    defineParam(multiply, "Multiply", 1.0f);
  }
```

如果你的内核有任何参数, 使用define函数给他们一个名字和默认值将会是个不错的练习。 如果没有任何参数, 就不需在你的内核中包含define函数。

## init()函数

init()函数将会在所有处理之前调用一次, 并且在它处理任何前期的初始化。 在反转内核中, __whitepoint_变量在这里初始化为浮点值1。

```C++
  void init() {
    _whiteAccessPoint = 1.0f;  //Local variables can be initialised here.
  }
```

还有其他的事情能在这里处理: 例如, 你能告诉编译器你想如何访问你的数据。 我们将在下个内核中看到。

如果不需要初始化, 你的内核中就不需要init()函数。

## process()函数

所有实际的工作都在process函数中进行。  在像素形式的内核中每个输出的像素都将调用它一次, 在分量形式的内核中每个输出组建都将调用它一次。 在反转内核中, 它看上去像这样:

```C++
  void process() {
    //Invert the input value from src and multiply:
    dst() = (_whiteAccessPoint - src()) * multiply;
   }
```

既然反转内核是分量形式的, 对于每个组件你都只能读取到相对应的输入。 `图像`的当前组件通过附加`()`来访问。 所以在这里, 用`dst()`访问输出图像的当前组件上的当前像素位置, 同时用`src()`访问输入图像当前组件的相同位置。 因为`src()`被特定为`eRead`, 我们只能从用`src()`读取`src`的值。 同时由于`dst`被特定为`eWrite`, 我们能向它写入。 还有第三种访问特定器`eReadWrite`可用, 他能让你同时读取和写入访问。通过这样给`dst()`赋值我们向`dst`写入数据:

```C++
    dst() = (_whiteAccessPoint - src()) * multiply;
```

为了反转输入图像的每个组件, 我们用局部变量`_whitePoint`减去`src`的值, 再乘以参数`multiply`。

改变此process函数的值将会改变内核执行的操作。 例如, 你可以通过直接无视`_whitePoint`, 直接将输入值乘以参数`multiply`, 这样就能得到一个"Gain"内核。 此时可以移除已经无用的`local`和`init()`代码段。 可以将`multiply` 参数重命名为`gain`, 给它一个其他的默认值, 还有为什么不给你的内核一个新的名字呢?

## 下一步

在[下一节](.\BoxBlurKernel.md)我们将会看到一个需要更复杂操作的模糊内核。