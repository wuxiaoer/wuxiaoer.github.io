---
layout: post
title: 机器学习之DT算法 
category: Tech 
tags: 
    - ML
    - DT
keywords: machine learning, DT
description:
---

# 机器学习之DT
------
DT是Decision Tree的缩写, 即决策树算法. DT算法是最常用的分类算法之一, 不用直到很多的机器学习知识就能理解决策树是如何工作的.

如下图所示
![DT_flowchart](/public/img/DT_flowchart.png)

上图中涉及如下概念:

决策块(decision block): 即上图中矩形框中的部分.

终止块(terminal block): 即上图中椭圆形中的部分, 表示决策的结果.

分支(branch): 上图中左右箭头所示.

上图中的决策树是一个邮件分类系统,
首先,检测邮件的发送地址,若是myEmployer.com,则分类为无聊时阅读.若不是, 进行右边分支决策, 判断是否包含hockey, 若包含hockey, 则分类为来自与朋友的email. 若不包含hockey,则分类为垃圾邮件,不需要阅读.

kNN是一种比较好的分类算法, 但是相对与DT, kNN不能从数据中获得任何的观点. 决策树的好处是人们可以很容易的就理解数据.

构建决策树的过程:
 1. 获取数据集
 2. 构建决策树
 3. 画出如上图所示的树

DT算法做了从数据中提取知识的事情. 从一大堆不熟悉的数据集中提取规则集. 机器学习即是机器从数据集中创建这些规则. 

以下从这三方面进行学习DT分类算法:

 - 讨论构建决策树的方法以及代码实现.
 - 决策树好坏的度量方法
 - 递归构建分类器并用matplotlib工具包画出来

## 决策树构建
DT算法
> * 优点: 计算量小,人们容易理解学习的结果, 丢失数值仍然OK, 可以处理不相关的特征.
> * 缺点: 易于过度拟合
> * 处理的数据类型: 数值型和标称型

在构建决策树过程中, 首先决定先用哪个特征值来划分数据集. 为此需要尝试每一个特征并度量哪一个用来划分数据可以得到最好的结果,基于选择的最好的特征把数据进行划分为子集. 子集将是第一个决策点的分支. 若分支中的所有数据所属与同一类,则不需要对子集进行再划分. 若不属于同一类, 则需要对子集进行再划分. 子集的划分与第一次划分的方式一样.重复该过程,直到所有的数据分类完成.

决策树的通用方法
> 1. 收集数据: 任何方法
> 2. 准备: 决策树构建算法只对标称型数据有效,因此任何连续的数值需要量化处理
> 3. 分析: 任何方法, 构建完决策树后应该可视化地来观察下构建的决策树
> 4. 训练: 构建树数据结构
> 5. 测试: 根据学习的树结构进行错误率计算
> 6. 使用: 该点可以在任何监督式学习任务中使用,决策树常常用来更好的理解数据

以下实现ID3算法

在决策树构建中, 要用到信息论知识来对数据集进行划分. 因此首先要介绍该知识,然后编码实现.

### 信息增益
我们选择一种方式把数据集进行划分,让数据从无序状态变得更加有组织. 有很多中方式来完成该任务. 且各自有各自的优缺点,  以下讲述的一种方式是对划分之前的信息进行度量.

#### 什么是信息增益
数据划分前后的信息的改变称之为**信息增益**(information gain)

当知道如何计算信息增益时,就可以根据每一个特征进行数据划分,然后查看哪个特征会得到最大的信息增益, 
**最大信息增益的划分就是最好的选择.**

#### 如何计算信息增益
在度量最好的划分以及划分数据之前, 我们需要直到如何计算信息增益. 集的信息度量称之为**香农熵**, 简称**熵**.
该名称来自与信息论之父, Claude Shannon.

**熵**: 定义为信息的期望值.
首先,我们需要定义信息. 若对多个值进行分类, 符号$x^{i}$信息定义为:
l(xi) = log2p(xi)
其中p(xi):选择类型为xi的概率

为了计算熵, 需要所有类别的所有可能值的所有信息的期望值.如下:

![information_gain_calc_formula](/public/img/information_gain_calc_formula.png)

其中n是类别数目.

以下通过python代码来计算信息熵.

首先创建数据集代码如下:

```python
def createDataSet():
    dataSet = [[1, 1, 'yes'],
            [1, 1, 'yes'],
            [1, 0, 'no'],
            [0, 1, 'no'],
            [0, 1, 'no']]
    labels = ['no surfacing' 'flippers']
    return dataSet, labels
```

该数据集即是下表所示的数据

![marine_animal_data](/public/img/marine_animal_data.png)

此处的数据集是比较简单的鱼类识别的数据.

计算信息熵的代码如下:

```python
from math import log

def calcShannonEnt(dataSet):
    numEntries  = len(dataSet)
    labelCounts = {}

    for featVec in dataSet:
        currentLabel = featVec[-1]
        if currentLabel not in labelCounts.keys():
            labelCounts[currentLabel] = 0;

        labelCounts[currentLabel] += 1

    shannonEnt = 0.0
    for key in labelCounts:
        prob = float(labelCounts[key]) / numEntries
        shannonEnt -= prob * log(prob, 2)

    return shannonEnt
```

在ipython中验证所写的python代码

```python
fatansy@fantasy:DT$ ipython
Python 2.7.8 (default, Jun 18 2015, 18:54:19) 
Type "copyright", "credits" or "license" for more information.

IPython 3.2.0 -- An enhanced Interactive Python.
?         -> Introduction and overview of IPython's features.
%quickref -> Quick reference.
help      -> Python's own help system.
object?   -> Details about 'object', use 'object??' for extra details.

In [1]: import createDataSet

In [2]: import calcShannonEnt

In [3]: myDat, labels = createDataSet.createDataSet()

In [4]: myDat
Out[4]: [[1, 1, 'yes'], [1, 1, 'yes'], [1, 0, 'no'], [0, 1, 'no'], [0, 1, 'no']]

In [5]: calcShannonEnt.calcShannonEnt(myDat)
Out[5]: 0.9709505944546686
```

熵值越高, 表示数据集越混乱,  
以下把数据集变得更加混乱, 看看熵是如何变化的.我们在添加第三类别, 

```python
In [6]: myDat[0][-1] = 'maybe'

In [7]: myDat
Out[7]: [[1, 1, 'maybe'], [1, 1, 'yes'], [1, 0, 'no'], [0, 1, 'no'], [0, 1, 'no']]

In [8]: calcShannonEnt.calcShannonEnt(myDat)
Out[8]: 1.3709505944546687
```

可见, 熵值变大了, 因为数据集变得更加混乱了.

以最大信息增益的方式对数据集进行划分. 但是我们事前是不知道的, 只有先划分后, 在进行计算信息增益.

另一种衡量数据无序的通用方式时**Gini impurity**. 它是从数据集中选择某一项的概率, 以及该项被错误划分的概率. 此处暂不讨论.

### 数据集划分

