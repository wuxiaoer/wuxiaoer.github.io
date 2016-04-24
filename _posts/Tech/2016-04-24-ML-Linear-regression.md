---
layout: post
title: 机器学习之线性回归
category: Tech 
tags: 
    - ML
    - Linear regression
keywords: machine learning, Linear regression
description:
---

# 机器学习之线性回归
------

## 线性回归参考
> * [machine learning](http://openclassroom.stanford.edu/MainFolder/DocumentPage.php?course=MachineLearning&doc=exercises/ex2/ex2.html)

> * [Deep learning](http://openclassroom.stanford.edu/MainFolder/DocumentPage.php?course=DeepLearning&doc=exercises/ex2/ex2.html)

## 线性回归python实现

```python

# -*- coding:utf-8 -*-
import numpy as np
import matplotlib.pyplot as plt
import mpl_toolkits.mplot3d
from matplotlib import cm

def loadDataSet(fileName):
    dataSet  = []
    fr = open(fileName)
    for line in fr.readlines():
        dataSet.append(float(line))
        
    return dataSet

x = loadDataSet("ex2x.dat")
y = loadDataSet("ex2y.dat")

# plot the training data
fig1 = plt.figure(1)
plt.scatter(x, y)
fig1.show()

# number of training example
m = len(x)

# Gradient descent
one = np.ones([m,])
x = np.array(x)
tmp = np.vstack((one,x))
x = tmp.T
x = np.matrix(x)

y = np.matrix(y).T

# initialize fitting parameters
theta = np.zeros([x.shape[1] , 1])
theta = np.matrix(theta)
MAX_ITR = 1500
alpha = 0.07

for iteration in range(MAX_ITR):
    grad = (1.0/m) * x.T * ((x * theta) - y); 
    theta = theta - alpha * grad

# print theta to screen
print theta

fig2 = plt.figure(2)
plt.plot(x[:,1], x * theta, '-', label="Linear regression")
plt.plot(x[:,1], y, 'o', label="training data")
plt.legend()
plt.xlabel('Age in years')
plt.ylabel('Height in meters')
fig2.show()

# Calculate J matrix
theta0_vals = np.linspace(-3, 3, 100)
theta1_vals = np.linspace(-1, 1, 100)

# Initialize J_vals to a matrix of 0's
J_vals = np.zeros((theta0_vals.size, theta1_vals.size))
J_vals = np.matrix(J_vals)

for i in range(theta0_vals.size):
    for j in range(theta1_vals.size):
        t = np.vstack((theta0_vals[i], theta1_vals[j]))
        t = np.matrix(t)
        J_vals[i, j] = (0.5 / m) * (x * t - y).T * (x * t - y)

fig3 = plt.figure(3)
ax = fig3.gca(projection='3d')
ax.plot_surface(theta0_vals, theta0_vals, J_vals, rstride=2, cstride=1, cmap=plt.cm.coolwarm, alpha=0.8)
fig3.show()

plt.show()
```

## 运行结果

训练样本散点和回归曲线预测图：

![linear_regression_result](/public/img/linear_regression_result.png)

损失函数与参数之间的曲面图:

![cost_function_pic](/public/img/linear_regression_cost_func_3d.png)

## 参考链接
[Deep learning：二(linear regression练习)](http://www.cnblogs.com/tornadomeet/archive/2013/03/15/2961660.html)

