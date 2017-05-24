[TOC]

# 通用命令

* ls

  列出对象

* select

  选择对象

* delete

  删除对象

* move

  移动几何对象的位置

* rename

  重命名

* sets

  创建集

* group

  编辑组

* ungroup

  解除所选对象的组

* makelive

  设置对象为live模式

* pixelMove

  基于像素的移动对象

- about

  显示版本信息

- quit

  退出程序

## 属性

* getAttr

* setAttr

* addAttr

* listAttr

* createNode

  创建节点

* connectAttr

  关联属性

* disconnectAttr

* copyAttr

### 常用属性

* defaultRenderGlobals

# MEL语言命令

## 字符串

* format

  格式化, 用^1, ^2...

## 脚本

* pause

  暂停

* isTrue

  测真

* setParent

  设置父级

# 动画

## 约束

* aimConstraint
* geometryConstraint
* normalConstraint
* orientConstraint
* parentConstraint
* pointConstraint
* pointOnPolyConstraint
* scaleConstraint
* tangentConstraint

# 渲染

* render

  开始/停止 maya software渲染

* hwrender

  硬件渲染

* batchRender

  批渲染

* doBlur

  将图像文件模糊

* callbacks

  设置回调

## 摄像机

* camera

  设置摄像机

* listCameras

  列出所有摄像机

* imagePlane

  设置图像平面

* cameraSet

  摄像机集

* panZoom

  平移缩放

* viewFit

  框显所选

## 层

* createRenderLayar

  创建渲染层

## 灯光

* ambientLight

* defaultLightListCheckBox

  为着色组创建是否连接至默认灯光列表的选框

* directionalLight

* exclusiveLightCheckBox

  为灯光创建是否从默认灯光列表中排除的选框

* lightlink

  设置灯光链接

* lightList

  添加/删除当前灯光关联的对象

* pointLight

* spotLight

* spotLightPreviewPort


# 系统

## 文件

* file

  打开/导入/导出/引用/保存/重命名文件

* chdir

  更改当前工作路径


* namespace

  设置命名空间

* setProject

  设置工程路径, 仅支持MEL

* fopen

* fprint

* fwrite

* fclose

* filetest

  文件检查

* incrementAndSaveScene

  增量保存, 仅支持MEL

* basename

  仅支持MEL

* dirname

  仅支持MEL

* exec

  执行命令, 仅支持MEL

  ​