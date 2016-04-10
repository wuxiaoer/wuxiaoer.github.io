---
layout: post
title: 机器学习之SVM算法 
category: Tech 
tags: 
    - ML
    - SVM
keywords: machine learning, SVM
description:
---

# 机器学习之SVM算法
------

SVM: Support Vector Machine的简称, 中文名:支持向量机
> * 优点: 低泛化错误, 计算开销不大, 容易解释结果
> * 缺点: 对参数调整和核函数的选择敏感, 基本SVM分类算法只能处理二类问题
> * 处理的数据类型: 数值型和标称型

## SVM相关概念
以下图中的数据为例,介绍SVM中涉及的相关概念

![svm-linear-separable](/public/img/svm-linear-separable.png)

**线性可分**: 上图中,可以通过一条直线就可以把方形点和圆形点分割开.这种情况称之为线性可分

**分离超平面**: 上图中把数据集分割开来的直线,即是分割超平面. 对于二维数据, 分割超平面是一条直线, 对于三维数据, 分割超平面是一个平面, 对于1024维数据, 分割超平面就是一个1023维的某对象来进行数据集进行分割.

**超平面**: 对于N维数据,其N-1维的对象就称之为超平面. 即分割的决策边界. 超平面的一边属于某一个类别, 另一侧所有数据属于另一个类别.

**间隔(margin)**: 离分割超平面最近的点, 确保他们到分割面的距离尽可能远, 此处点到分割面的距离称之为间隔.

**支持向量(support vector)**:离分离超平面最近的点.


如上图中所示,B-D图中的三条直线都可以对数据集进行分割, 那么哪一种分割是最好的呢? 这就是接下来要讲的最大化分割直线到支持向量的数据. 以下试图找到优化该问题的方法.

**SVM算法实现的通用框架**
> 1. 收集数据: 可以使用任意方法
> 2. 准备数据: 需要数值型数据
> 3. 分析数据: 有助于可视化分割超平面
> 4. 算法训练: SVM的大部分时间来自于训练, 该过程主要实现两个参数的调优
> 5. 算法测试: 十分简单的计算过程就可以实现
> 6. 使用算法: 几乎所有分类问题都可以使用SVM, 需要注意的是,SVM本身是二类分类器,对于多类问题,若要使用SVM,需要对代码做一些修改

## 寻找最大间隔
以下图中所示数据集为例

![svm-maximum-margin](/public/img/svm-maximum-margin.png)

如何衡量分割直线能最好的把给定数据集进行分割呢?

分割超平面用公式表达的形式为: w^Tx + b
若要找到图中A点到分割平面的距离, 需要对A点到分割平面的法线(或垂直线)进行计算, 根据高等数学中的知识,可知距离的计算公式为: |w^Tx + b|/||w||.

此处b类似于逻辑回归中的截距w0, 向量w和b描述了给定数据的分割线或超平面.

## SMO高效优化算法

根据前面的两个式子进行优化,

一个是:最小化的目标函数

另一个是: 优化过程中须要遵循的约束条件.

以下介绍SMO算法
SMO: 序列最小优化(Sequential Minimal Optimization). SMO算法将大的优化问题分解为多个小优化问题来求解. 这些小的优化问题很容易求解. 

SMO算法的目标是求出一系列的alpha和b, 一旦求出了这些alpha, 就可以很容易计算处权重向量w,并得到分割超平面.

### 导入数据以及处理
从文件中导入数据的程序如下

```python
def loadDataSet(fileName):
    dataMat  = []
    labelMat = []
    fr = open(fileName)
    for line in fr.readlines():
        lineArr = line.strip().split('\t')
        dataMat.append([float(lineArr[0]), float(lineArr[1])])
        labelMat.append(float(lineArr[2]))
    return dataMat,labelMat

def selectJrand(i, m):
    j = i #we want to select any J not equal to i
    while (j == i):
        j = int(random.uniform(0,m))
    return j

def clipAlpha(aj,H,L): #clips alpha values that are greater than H or less than L
    if aj > H: 
        aj = H
    if L > aj:
        aj = L
    return aj    
```

程序解析:

> readlines()函数: 一次读取整个文件, readlines() 自动将文件内容分析成一个行的列表，该列表可以由 Python 的 for ... in ... 结构进行处理
>
> readline()函数: 每次只读取一行，通常比 .readlines() 慢得多。仅当没有足够内存可以一次读取整个文件时，才应该使用 .readline()
>
> random.uniform(a, b): 用于生成一个指定范围内的随机符点数，两个参数其中一个是上限，一个是下限。如果a < b，则生成的随机数n: a <= n <= b。 如果 a > b， 则 b <= n <= a

导入的数据如下图所示

![svm-smo-simple-data](/public/img/svm-smo-simple-data.png)

### SMO算法实现

```python
def smoSimple(dataMatIn, classLabels, C, toler, maxIter):
    dataMat    = mat(dataMatIn)
    labelMat   = mat(classLabels).transpose()
    b          = 0
    m,n        = shape(dataMat)
    alphas 	   = mat(zeros((m,1)))
    iter 	   = 0
    while (iter < maxIter):
        alphaPairsChanged = 0
        for i in range(m):
            fXi = float(multiply(alphas, labelMat).T*(dataMat * dataMat[i,:].T)) + b
            Ei = fXi - float(labelMat[i])#if checks if an example violates KKT conditions
            if ((labelMat[i]*Ei < -toler) and (alphas[i] < C)) or ((labelMat[i]*Ei > toler) and (alphas[i] > 0)):
                j = selectJrand(i,m)
                fXj = float(multiply(alphas,labelMat).T*(dataMat*dataMat[j,:].T)) + b
                Ej = fXj - float(labelMat[j])
                alphaIold = alphas[i].copy(); alphaJold = alphas[j].copy();
                if (labelMat[i] != labelMat[j]):
                    L = max(0, alphas[j] - alphas[i])
                    H = min(C, C + alphas[j] - alphas[i])
                else:
                    L = max(0, alphas[j] + alphas[i] - C)
                    H = min(C, alphas[j] + alphas[i])
                if L==H: print "L==H"; continue
                eta = 2.0 * dataMat[i,:]*dataMat[j,:].T - dataMat[i,:]*dataMat[i,:].T - dataMat[j,:]*dataMat[j,:].T
                if eta >= 0: print "eta>=0"; continue
                alphas[j] -= labelMat[j]*(Ei - Ej)/eta
                alphas[j] = clipAlpha(alphas[j],H,L)
                if (abs(alphas[j] - alphaJold) < 0.00001): print "j not moving enough"; continue
                alphas[i] += labelMat[j]*labelMat[i]*(alphaJold - alphas[j])#update i by the same amount as j
                                                                        #the update is in the oppostie direction
                b1 = b - Ei- labelMat[i]*(alphas[i]-alphaIold)*dataMat[i,:]*dataMat[i,:].T - labelMat[j]*(alphas[j]-alphaJold)*dataMat[i,:]*dataMat[j,:].T
                b2 = b - Ej- labelMat[i]*(alphas[i]-alphaIold)*dataMat[i,:]*dataMat[j,:].T - labelMat[j]*(alphas[j]-alphaJold)*dataMat[j,:]*dataMat[j,:].T
                if (0 < alphas[i]) and (C > alphas[i]): b = b1
                elif (0 < alphas[j]) and (C > alphas[j]): b = b2
                else: b = (b1 + b2)/2.0
                alphaPairsChanged += 1
                print "iter: %d i:%d, pairs changed %d" % (iter,i,alphaPairsChanged)
        if (alphaPairsChanged == 0): 
        	iter += 1
        else: 
        	iter = 0
        print "iteration number: %d" % iter
        
    return b, alphas
```

程序解析

>待补充

该函数的使用

```python

```



## 参考
- [Python中的random模块](http://fulerbakesi.iteye.com/blog/1589097)
