---
published: true
layout: post
title: web scraping常用Python库
category: Tech 
tags: 
  - scikit-learning
  - urllib
  - Beautifulsoup
  - Python
time: 2016.03.18 23:02:45
excerpt: NULL
---

## web scraping常用python库
常用的python库有urllib, urlopen, BeautifulSoup等

### urllib:
标准的python库(即不需要额外的安装该库), 其中包含请求网页数据, 处理cookies, 甚至改变诸如headers和用户代理的元数据的函数

### urlopen:
通过网络打开一个远程对象,并读取.它是一个非常通用的库(可以读取HTML文件, 图像文件,或其他文件流), 后续会频繁的用到该函数.

### BeautifulSoup:

#### 安装BeautifulSoup
对于Linux系统
>sudo apt-get install python-bs4

对于MAC系统
首先安装python包管理工具pip
>sudo easy_install pip

然后通过pip安装BeautifulSoup
>pip install beautifulsoup4

当安装BeautifulSoup包时,需要按照如下方式安装,不然可能会安装在python 2.x, 而不是python 3.x
>sudo python3 setup.py install

若使用的是pip来安装,需要使用pip3来安装python 3.x版本的包
>pip3 install beautifulsoup4

安装完后,在python中就能识别该BeautifulSoup库了

#### BeautifulSoup包测试
> from bs4 import BeautifulSoup

若没有出现找不到该库的错误,则说明安装成功

> Traceback (most recent call last):
>      File "<stdin>", line 1, in <module>
>      ImportError: cannot import name 'BeautifulSoup'
      
#### BeautifulSoup包的使用
{% highlight python lineno %}
   from urllib.request import urlopen
   from bs4 import BeautifulSoup
   html = urlopen("http://www.pythonscraping.com/exercises/exercise1.html")
   bsObj = BeautifulSoup(html.read())
   print(bsObj.h1)
{% endhighlight %}

程序输出:

> <h1>An Interesting Title<h1>

