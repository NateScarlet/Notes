

# UnityEngine 包

* Start()

  对象初始化时运行的脚本,同`__init__()`

* Update ()

  渲染帧时被调用

* FixedUpdate ()

  物理计算时调用

* GetComponent<Rigidbody>()

  返回同一物件下的Rigidbody对象

# 类型

* Vector3

  3维向量

# Input 类

GetAxis ()

获取控制轴

# Rigidbody 类

## 变量

| 名称       | 说明    |
| -------- | ----- |
| mass     | 刚体的重量 |
| position | 刚体的位置 |
| rotation | 刚体的旋转 |
| velocity | 刚体的速度 |

## 公共函数

* AddForce 

  施加力


* MovePosition

  移动位置

* MoveRotation

  移动旋转

* Sleep

  强制停止刚体至少一帧

* WakeUp

  强制唤醒刚体