| rank | ▲ | ✰ | vote | url |
|:-:|:-:|:-:|:-:|:-:|
|  13  |  811 | 323 | 639 | [url](http://stackoverflow.com/questions/1132941/least-astonishment-in-python-the-mutable-default-argument) |

***

## Python中的"小震撼":变化的默认参数

许多使用很长时间Python的人也被下面的问题困扰:

```python
def foo(a=[]):
    a.append(5)
    return a
```

Python新手估计可能会想这个函数返回一个只有元素`[5]`的列表.但是结果却出人意料:

```python
>>> foo()
[5]
>>> foo()
[5, 5]
>>> foo()
[5, 5, 5]
>>> foo()
[5, 5, 5, 5]
>>> foo()
```

我的一个经理曾经碰到过这个特性并把它叫做语言的"动态设计缺陷".这个现象应当有更深层次的解释,如果你不懂它的内部它确实非常令人困惑.然而我不能回答下面的问题:是什么原因使默认参数在函数的定义时被绑定,而不是在执行时?我怀疑这个特性在现实中有没有实际的用途(就像在C语言中有谁去用静态变量?)

***

事实上这并不是设计缺陷,也不是什么内部或性能原因.

原因很简单,Python中的函数是最高等级的对象,而不仅仅是一小段代码.

试着这么来理解:**一个函数是一个被它自己定义而执行的对象;默认参数是一种"成员数据",所以它们的状态和其他对象一样,会随着每一次调用而改变.**

Effbot在它的[Python中的默认参数](http://effbot.org/zone/default-values.htm)对这种行为的原因解释的非常清楚!我强烈建议你读一读能对函数对象的工作有更深一步的了解.



