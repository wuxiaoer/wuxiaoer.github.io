---
published: true
layout: post
title: Ubuntu下scikit-learning包的安装
category: Tech 
tags: 
  - scikit-learning
  - Python
time: 2016.03.18 23:02:45
excerpt: NULL
---
## scikit-learn工具包安装

##### 下载地址
```
https://pypi.python.org/pypi/scikit-learn/0.17.1
```

##### 解压
```
$ tar zxvf scikit-learn-0.17.1.tar.gz
```

##### 安装
从源码安装scikit-learn时,依赖numpy和scipy, 因此需要先安装numpy和scipy
```
$ python setup.py build
$ sudo python setup.py install
```

##### 测试
安装完成后,在源代码目录外的其他地方启动测试(注:需要安装nose包):
```
$ nosetests -v sklearn
```
