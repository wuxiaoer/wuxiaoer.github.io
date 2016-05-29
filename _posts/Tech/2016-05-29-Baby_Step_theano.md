---
layout: post
title: 如何使用theano进行两个数相加
category: Tech 
tags: 
    - theano
keywords: theano
description:
---

# 两个标量相加
首先，我们从一个简单的函数：两个数相加，来初步了解下Theano是怎么使用的。

```
In [1]: import numpy

In [2]: import theano.tensor as T

In [3]: from theano import function

In [4]: x = T.dscalar('x')

In [5]: y = T.dscalar('y')

In [6]: z = x + y

In [7]: f = function([x, y], z)

```

然后，我们使用上面创建的函数

```
In [10]: f(2,3)
Out[10]: array(5.0)

In [11]: numpy.allclose(f(16.3, 12.1), 28.4)
Out[11]: True
```

以下分步对以上代码进行讲解，第一步是定义两个符号（变量），表示要相加的值。从现在开始，我们将使用术语变量来表示“符号”（也就是说，x，y，z都是变量对象）， 函数f的输出是0维的numpy.ndarray.

如果你按上述步骤在解释器（例如ipython）中输入代码时，你将注意到在执行function指令时，会有一个小小的延时， 这背后是因为函数f正在被编译为C代码。


### 步骤1

```
In [4]: x = T.dscalar('x')

In [5]: y = T.dscalar('y')
```

解释：
在Theano中，所有的符号必须是有类型的，T.dscalar是分配给“doubles(d)的0维数组（标量）”的类型， 它是Theano的类型。

dscalar不是一个类，因此，x和y实际上都不是dscalar的实例。它们是TensorVariable的实例， 然后，x和y分配为dscalar的类型。 如下

```
In [12]: type(x)
Out[12]: theano.tensor.var.TensorVariable

In [13]: x.type
Out[13]: TensorType(float64, scalar) 

In [14]: T.dscalar
Out[14]: TensorType(float64, scalar)

In [15]: x.type is T.dscalar
Out[15]: True
```

通过传入字符串参数调用T.dscalar， 创建一个给定名字的浮点标量的变量。若不传入参数，该符号将是无名字的。不过名字不是必须的，但是便于调试。

后面将讲解Theano的内部结构，更多的内容可以查看[Graph Structure](http://deeplearning.net/software/theano/extending/graphstructures.html#graphstructures)


### 步骤2
第二步计算x和y为z

```
In [6]: z = x + y
```

z是另一个变量，表示x和y的和， 可以使用pp函数可以很好的打印出z相关的计算

```
In [18]: from theano import pp

In [19]: print(pp(z))
(x + y)
```


### 步骤3
最后一步是创建一个函数， x和y作为输入， z作为输出。

[function](http://deeplearning.net/software/theano/library/compile/function.html#function.function)的第一个参数是一个变量列表作为函数的输入。第二个参数是一个单变量或者变量列表。 第二个变量作为我们应用该函数时我们想要看的输出。然后，f的使用与普通的python函数一样。




