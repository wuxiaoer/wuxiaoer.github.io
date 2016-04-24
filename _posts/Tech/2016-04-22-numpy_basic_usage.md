---
layout: post
title: python numpy学习记录
category: Tech 
tags: 
    - Python
    - numpy
keywords: Python, numpy
description:
---

### array数组

numpy中最基本的类型是array. 其相关操作都是按元素操作的(+, -, *, /等), 
举例:

```python
fatansy@fantasy:Ex1_Linear_regression$ ipython
Python 2.7.8 (default, Jun 18 2015, 18:54:19) 
Type "copyright", "credits" or "license" for more information.

IPython 3.2.0 -- An enhanced Interactive Python.
?         -> Introduction and overview of IPython's features.
%quickref -> Quick reference.
help      -> Python's own help system.
object?   -> Details about 'object', use 'object??' for extra details.

In [1]: import numpy as np

In [2]: a = np.arr
np.array         np.array2string  np.array_equal   np.array_equiv   np.array_repr    np.array_split   np.array_str

In [2]: a = np.array([1,2])

In [3]: a
Out[3]: array([1, 2])

In [4]: b = np.array([2,3])

In [5]: b
Out[5]: array([2, 3])

In [6]: c = a * b

In [7]: c
Out[7]: array([2, 6])

In [8]: np.dot(a, b)
Out[8]: 8
```

注: 两个array相乘*指的是对应元素相乘;
两个array的dot表示矩阵相乘

> * 若a是array, 那么a.T表示转置
> * 把array转为matrix, 使用asmatrix()
> * 多数numpy函数返回的是array类型,不是matrix类型


