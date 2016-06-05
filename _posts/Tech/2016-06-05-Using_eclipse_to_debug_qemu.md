---
layout: post
title: 使用Eclipse调试Qemu及Linux Kernel
category: Tech 
tags: Qemu
keywords: Eclipse，Qemu
description:
---

## 下载Qemu代码

1. 下载版本

下载qemu-2.6.0版本代码，[下载地址](http://wiki.qemu-project.org/download/qemu-2.6.0.tar.bz2)


2. 解压

> tar jxvg qemu-2.6.0.tar.bz2


3. 配置

配置命令如下

> ./configure --prefix=/home/fantasy/opt/qemu --target-list="arm-softmmu i386-softmmu x86_64-softmmu arm-linux-user i386-linux-user x86_64-linux-user"

注: Qemu相关的操作到此为止


## 下载Eclipse for C/C++工具

用于C/C++的Eclipse[下载地址](http://ftp.yz.yamagata-u.ac.jp/pub/eclipse//technology/epp/downloads/release/luna/SR2/eclipse-cpp-luna-SR2-linux-gtk-x86_64.tar.gz)

下载完后，直接解压，运行其中的Eclipse文件即可。


## Eclipse中导入Qemu源码。

1. 打开Eclipse后，执行File->import->C/C++ -> Existing Code as Makefile Project. 点击Next


2. 选择Qemu源码所在的目录，工具链选择Linux GCC. 如下图
  ![eclipse_import_qemu_src](/public/img/eclipse_import_cpp_project.png)

3. 然后在进行build project

可能会出现找不到autoreconf工具，那么安装如下package即可。

> sudo apt-get install autoconf libtool

