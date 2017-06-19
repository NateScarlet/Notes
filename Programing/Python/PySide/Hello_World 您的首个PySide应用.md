# 您的第一个PySide应用程序

如果您按照[Setting_up_PySide](http://wiki.qt.io/Setting_up_PySide) Wiki页面安装PySide，您现在应该在您的计算机上拥有完整的PySide副本，以开始开发Qt + Python GUI应用程序。 与任何其他编程框架一样，您从传统的“Hello World”程序开始。

以下是PySide中Hello World的简单示例：

```
#!/usr/bin/python

# Import PySide classes
import sys
from PySide.QtCore import *
from PySide.QtGui import *

# Create a Qt application
app = QApplication(sys.argv)
# Create a Label and show it
label = QLabel("Hello World")
label.show()
# Enter Qt application main loop
app.exec_()
sys.exit()
```

使用PySide桌面应用程序，您必须始终通过导入PySide.QtCore和PySide.QtGui类来启动文件。 这些类具有构建PySide应用程序的主要功能。 例如，PySide.QtGui包含处理小部件的功能，而PySide.QtCore包含处理信号和插槽的方法以及控制应用程序。

导入后，您将创建一个QApplication，它是主要的Qt应用程序。 由于Qt可以从命令行接收参数，因此必须将任何参数传递给QApplication对象。 通常，您不需要传递任何参数，因此您可以保留原样。

创建应用程序对象后，我们创建了一个QLabel对象。 QLabel是一个可以显示文本（简单或丰富，如html）和图像的小部件。 请注意，在创建标签之后，我们将调用方法**show**来显示用户的标签。

最后，我们调用**app.exec_()**，它将进入Qt主循环并开始执行Qt代码。 在现实中，只有这样才能显示标签，但现在可以忽略。

## 在标签中显示html

如前所述，您可以在标签中插入html标签来显示富文本。 尝试更改创建标签的代码，例如：

```
label = QLabel("<font color=red size=40>Hello World</font>")

```

你会看到“Hello World”现在更大和更红。 你可以尝试改变另一种颜色，另一种尺寸，或让它闪烁！ 或者您可以创建其他元素而不是QLabel，如QPushButton或其他元素。