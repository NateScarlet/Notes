# 您的第一个应用程序使用PySide和QtQuick / QML

QML是一种声明式语言，用于描述程序的用户界面：它的外观以及它的行为。 在QML中，用户界面被指定为具有属性的对象树。 在本教程中，我们将展示如何使用PySide和QML创建一个简单的**Hello World**应用程序。

PySide / QML应用程序至少包含两个不同的文件 - 一个包含用户界面QML描述的文件，以及加载qml文件的python文件。 为了避免现在的问题，不要忘记这两个文件保存在同一文件夹中。

这是一个简单的QML文件，名为**view.qml**：

```
import QtQuick 1.0

Rectangle {
 width: 200
 height: 200
 color: "red"

Text {
 text: "Hello World"
 anchors.centerIn: parent
 }
}
```

我们从import QtQuick 1.0开始，因为从理论上来说，QtQuick与Qt / PySide有不同的发布时间表。

对于以前使用HTML或XML文件的人来说，其余的QML代码是非常简单的。 基本上，我们正在创建一个大小为200 * 200的红色矩形，并且在该矩形内，我们正在添加一个说“**Hello World**”的Text元素。 代码**anchors.centerIn: parent**只是使文本以其直接父对象为中心。

现在，让我们来看看在PySide中的代码。 我们称之为**main.py**：

```
#!/usr/bin/env python
# -'''- coding: utf-8 -'''-

import sys
from PySide.QtCore import *
from PySide.QtGui import *
from PySide.QtDeclarative import QDeclarativeView

# Create Qt application and the QDeclarative view
app = QApplication(sys.argv)
view = QDeclarativeView()
# Create an URL to the QML file
url = QUrl('view.qml')
# Set the QML file and show
view.setSource(url)
view.show()
# Enter Qt main loop
sys.exit(app.exec_())
```

如果您已经熟悉PySide并遵循了我们的教程，这些代码中的大部分已经很熟悉了。 唯一的新奇之处在于，您必须导入QDeclarativeView并将QDeclarativeView对象的源设置为QML文件的URL。 那么，像任何Qt小部件一样，你调用**QDeclarativeView.show()**。

**提示：**如果您是为桌面编程，您应该考虑在显示视图之前添加 **view.setResizeMode(QDeclarativeView.SizeRootObjectToView)** 。 这将强制外部QML矩形与外部窗口一起调整大小。