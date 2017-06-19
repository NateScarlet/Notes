该Wiki页面列出了在开始使用PySide开发时可能遇到的常见缺陷。 如果你体验到一些“哦！” 在使用PySide开发应用程序的时刻，请在这里记录问题。

## 参考

如果QObject在Python中超出范围，它将被删除。 你必须保留对对象的引用：

- 将其存储为您保留的对象的属性，例如

  ```
  self.window = QMainWindow()
  ```

- 将父QObject传递给对象的构造函数，因此它由父对象拥有

**这不行：**

```python
class MyStuff(object):
   # …
   def animate_stuff(self, target):
      animation = QtCore.QPropertyAnimation(target, 'rotation')
      animation.setDuration(700)
      animation.setEasingCurve(QtCore.QEasingCurve.OutSine)
      animation.setEndValue(100)
      animation.start(QtCore.QAbstractAnimation.DeleteWhenStopped)
```

原因是将在`animate_stuff()`最后删除动画, 所以真的没有机会做任何事情。 在动画（通常有一个目标QObject）的情况下，通过将父作为最后一个参数赋予构造函数，使其成为父项的子项是个好主意：

```python
class MyStuff(object):
   # …
   def animate_stuff(self, target):
      animation = QtCore.QPropertyAnimation(target, 'rotation', target)
      # …
```

This will work, because the animation reference is now owned by "target". Another option is to save the animation as an attribute of the object (using "self.animation = …"). This way, the reference to the animation is kept around as long as the object that has the attribute (if it does not get deleted manually before). Be aware that overwriting the attribute (e.g. with another animation while the first animation is still running) will again cause all references for the object to be removed, therefore deleting the object again.

## QtCore.QObject.sender()

If you want to get the object that emitted a signal, you can do so using

```
QtCore.QObject.sender()
```

, although you should really think twice before using it (see the API docs of QObject for details). If you really, really decide that you have to use it, be aware that right now, you cannot call it as a static method, but only from within a QObject slot.

This means that **the following code won't work**:

```python
def on_signal(*args):
   print args
   print QtCore.QObject.sender() # THIS DOES NOT WORK!

a.someSignal.connect(on_signal)
```

To achieve the same effect, you have to create a QObject subclass with a Slot and access sender() as a member method of your object, like this:
```python
class Listener(QtCore.QObject):`
  @QtCore.Slot()
  def on_signal(self, *args):
     print args
     print self.sender()
listener = Listener() a.someSignal.connect(listener.on_signal)
```