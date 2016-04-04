---
published: true
layout: post
title: C语言中constructor和destructor的用法
category: Tech 
tags: 
  - C
time: 2016.03.18 23:02:45
excerpt: NULL
---

__ attribute __((constructor)): 在main函数被调用之前调用
注:调用之前，各个全局变量已经完成初始化。也就是说，这些函数是在全局变量初始化之后，main函数之前调用的。这一点是非常重要的，否则可能会引起很多的问题。

__ attribute __((destructor)):  在main函数被调用之后调用

例子
{% highlight c %}
#include<stdio.h>

__attribute__((constructor)) void before_main() 
{
    printf("before main\n");
}

 __attribute__((destructor)) void after_main() 
{
    printf("after main\n");
}
/* 主函数 */
 int main(int argc, char **argv) 
{
    printf("in main\n");
    return 0;
}

{% endhighlight %}

参考:
[__attribute__中constructor和destructor[总结]](http://www.cnblogs.com/Anker/p/3462363.html)
