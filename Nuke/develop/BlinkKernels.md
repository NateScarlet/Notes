# 内核(Kernel)介绍

我们首先将要认识是一个简单将单个图像作为输入, 反转它的颜色, 然后乘以某个值最后写入输出图像的内核。 

# 反转内核(InvertKernel)

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

# 内核与迭代

Blink内核以和C++相似的方式声明:

```C++
kernel InvertKernel : ImageComputationKernel<eComponentWise>
```

这一行告诉我们反转内核是一个blink"内核", 和C++的类很相似。这个Blink内核从_ImageComputationKernel_继承, 它是一个用于生成输出图像的内核。 这个内核采用分量形式(componentwise)的行为(_eCompnentWise_)。 分量形式意味着输出图像的每个通道将会被单独处理。 当处理每个通道时, 只有相对应通道的的输入数据能被访问。

一个备选方案是使用像素形式(pixelwise)的内核(_ePixelWise_)。像素形式的内核能在每个像素输出到所有通道并且能访问输入数据的所有通道。你应该为任何涉及多个通道互相影响的操作使用像素形式的内核, 比如饱和度调整。一个像素形式的内核像这样声明:

```C++
kernel SaturationKernel : ImageComputationKernel<ePixelWise>
```

当使用图像处理内核(ImageComputationKernel)时, 你不能控制处理输出像素(对于像素形式内核)或者输出组件(对于分量形式内核)的顺序。 内核调用会对输出空间的每一点都进行。 目的是所有的内核调用都是互相独立并且可同时进行的。 最少在GPU上, 上千的内核调用会同时进行。 我们的反转内核就是个这种方式的例子: 每个输出值都能单独计算, 并不依赖输出的其他值。 事实上, 许多图像处理操作都差不多能直接映射到平行处理模型。



# 图像指定

在内核结构(body)内部我们需要指定它需要的图像。 反转内核有一个输入src和一个输出图像dst, 像这样声明:

```C++
  Image<eRead, eAccessPoint, eEdgeClamped> src;  //the input image
  Image<eWrite> dst;  //the output image
```

这告诉我们src是一个_Image_类对象, 并且_eRead_告诉我们对这个图像仅读取访问。 dst同样是一个_Image_类对象但是我们需要写入访问_eWrite_.

在图像指定时你能告诉编译器更多你想要如何访问图像和当你想访问图像范围外时应该怎么做。例如, 在反转内核中输入图像有_eAccessPoint_访问, 这意味着他只在输出图像的当前位置才会访问。 它还有一个边缘方法_eEdgeClamped_定义了边缘外的像素将会用边缘像素进行重复。我们将在下一节看到更多关于图像指定器的例子。

所有的内核都应该有至少一个输出图像, 你应该用这样的一行来定义:

```C++
Image<eWrite> dst;
```

# 参数

内核的参数将在_param_代码段中定义, 和你在C++类中定义成员变量时一样。 如果你的内核不需要任何参数, 你可以忽略这一代码段。

反转内核只有一个参数_multiply_:

```C++
  param:
    float multiply;  //This parameter is made available to the user.
```

当内核被编译在一个BlinkScript节点内时, 节点将会为内核的每个参数生成一个调整参数(knob), 并且将它添加到**Kernel Parameters**标签页中。 一当创建, 节点将只有一个参数**Multiply**。

内核参数可以是C++内置类型例如float或者int。 还支持向量参数: float2, float3 及 float4, 他们分别代表了2、3、4维向量, 并且类似的还有 int2, int3, int4。同样支持 float3x3(3x3矩阵) 及 float4x4(4x4矩阵) 矩阵类型。

# 局部变量

你能在内核的_local_代码段中添加不显示给用户的局部变量。 当然如果你不想要使用局部参数, 你可以忽略这一代码段。

反转内核只有一个局部变量__whitePoint_。 它用来