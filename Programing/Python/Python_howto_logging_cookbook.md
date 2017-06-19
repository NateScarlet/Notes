# Logging 菜谱

[TOC]



## 1.在多个模块中使用logging

对`logging.getLogger(’someLogger’)`的多个调用会返回同一个logger对象。不仅在同一个模块内是这样, 只要是在同一个Python解释器进程中,都会返回同一个logger对象。它可以引用同一个对象: 而且, 应用编码在能够同一个模块中定义和设置它的父logger,及在另外的模块中创建(但不能设置)它的子logger,并且所有对子logger的调用将会传达到父, 以下是main模块:

```python
import logging
import auxiliary_module
# create logger with 'spam_application'
logger = logging.getLogger('spam_application')
logger.setLevel(logging.DEBUG)
# create file handler which logs even debug messages
fh = logging.FileHandler('spam.log')
fh.setLevel(logging.DEBUG)
# create console handler with a higher log level
ch = logging.StreamHandler()
ch.setLevel(logging.ERROR)
# create formatter and add it to the handlers
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
fh.setFormatter(formatter)
ch.setFormatter(formatter)
# add the handlers to the logger
logger.addHandler(fh)
logger.addHandler(ch)
logger.info('creating an instance of auxiliary_module.Auxiliary')
a = auxiliary_module.Auxiliary()
logger.info('created an instance of auxiliary_module.Auxiliary')
logger.info('calling auxiliary_module.Auxiliary.do_something')
a.do_something()
logger.info('finished auxiliary_module.Auxiliary.do_something')
logger.info('calling auxiliary_module.some_function()')
auxiliary_module.some_function()
logger.info('done with auxiliary_module.some_function()')
Here is the auxiliary module:
import logging
# create logger
module_logger = logging.getLogger('spam_application.auxiliary')
class Auxiliary:
def __init__(self):
self.logger = logging.getLogger('spam_application.auxiliary.Auxiliary')
self.logger.info('creating an instance of Auxiliary')
def do_something(self):
self.logger.info('doing something')
a = 1 + 1
self.logger.info('done doing something')
def some_function():
module_logger.info('received a call to "some_function"')
```

输出将会像是这样:

```python
2005-03-23 23:47:11,663 - spam_application - INFO -
creating an instance of auxiliary_module.Auxiliary
2005-03-23 23:47:11,665 - spam_application.auxiliary.Auxiliary - INFO -
creating an instance of Auxiliary
2005-03-23 23:47:11,665 - spam_application - INFO -
created an instance of auxiliary_module.Auxiliary
2005-03-23 23:47:11,668 - spam_application - INFO -
calling auxiliary_module.Auxiliary.do_something
2005-03-23 23:47:11,668 - spam_application.auxiliary.Auxiliary - INFO -
doing something
2005-03-23 23:47:11,669 - spam_application.auxiliary.Auxiliary - INFO -
done doing something
2005-03-23 23:47:11,670 - spam_application - INFO -
finished auxiliary_module.Auxiliary.do_something
2005-03-23 23:47:11,671 - spam_application - INFO -
calling auxiliary_module.some_function()
2005-03-23 23:47:11,672 - spam_application.auxiliary - INFO -
received a call to 'some_function'
2005-03-23 23:47:11,673 - spam_application - INFO -
done with auxiliary_module.some_function()
```



## 2.在多个线程中使用logging

在多个线程中使用logging将不需要额外的付出。 下例展示了从main(初始)线程和其他线程中进行logging的方法:

```python
import logging
import threading
import time

def worker(arg):
while not arg['stop']:
logging.debug('Hi from myfunc')
time.sleep(0.5)
def main():
logging.basicConfig(level=logging.DEBUG, format='%(relativeCreated)6d %(threadName)s %(message)s')
info = {'stop': False}
thread = threading.Thread(target=worker, args=(info,))
thread.start()
while True:
try:
    logging.debug('Hello from main')
    time.sleep(0.75)
    except KeyboardInterrupt:
    info['stop'] = True
    break
    thread.join()
if __name__ == '__main__':
    main()
When run, the script should print something like the following:
   0 Thread-1 Hi from myfunc
   3 MainThread Hello from main
 505 Thread-1 Hi from myfunc
 755 MainThread Hello from main
1007 Thread-1 Hi from myfunc
1507 MainThread Hello from main
1508 Thread-1 Hi from myfunc
2010 Thread-1 Hi from myfunc
2258 MainThread Hello from main
2512 Thread-1 Hi from myfunc
3009 MainThread Hello from main
3013 Thread-1 Hi from myfunc
3515 Thread-1 Hi from myfunc
3761 MainThread Hello from main
4017 Thread-1 Hi from myfunc
4513 MainThread Hello from main
4518 Thread-1 Hi from myfunc
This shows the logging output interspersed as one might expect. This approach works for more threads than shown
here, of course.
```



