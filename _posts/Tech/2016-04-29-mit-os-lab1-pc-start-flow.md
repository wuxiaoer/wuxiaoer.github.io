---
layout: post
title: MIT OS课程之实验1-PC启动流程
category: Tech
tags: os
keywords: mit, os
description:
---

# 简介
------
该部分实验分为3部分:

> 第1部分: 熟悉x86汇编, QEMU x86仿真器, PC上电启动过程


> 第2部分: 学习6.828内核的启动加载代码, 该部分代码在boot目录中.


> 第3部分: 研究6.828内核的初始化部分(JOS). 该部分代码在kernel目录中.

# 第1部分: PC启动
------
第一个练习的目的用来介绍x86汇编语言和PC启动引导过程, 以及熟悉QEMU和QEMU/GDB调试. 
该部分不需要编写代码. 但是必须要理解该部分的代码, 以及能回答提出来的问题.

## 2.1 熟悉x86汇编
若还不熟悉x86汇编语言,在该课程中要快速的熟悉起来, 可以从如下的书本开始

课本:[PC Assembly Language book](https://pdos.csail.mit.edu/6.828/2014/readings/pcasm-book.pdf)

警告:

该书中的例子使用NASM汇编写的,而我们将使用GNU汇编. NASM使用intel语法格式,GNU汇编使用的是AT&T语法, 但是语义上是相同的. 这两种汇编语法之间的转换非常简单,可以参考[Brennan's Guide to Inline Assembly](www.delorie.com/djgpp/doc/brennan/brennan_att_inline_djgpp.html)

练习1:

熟悉6.828参考页上的[汇编语言材料](https://pdos.csail.mit.edu/6.828/2014/reference.html), 当阅读和编写x86汇编时,会用到这些材料.

强烈推荐阅读[Brennan's Guide to Inline Assembly](www.delorie.com/djgpp/doc/brennan/brennan_att_inline_djgpp.html)中的”The Syntax”部分, 对AT&T汇编语法进行了很多(同时简洁)的描述. 同时在JOS实验中使用GNU汇编器.

## 2.2 仿真x86
使用仿真软件来模拟一个真实的PC, 简化调试, 例如在仿真的x86中设置断点. 而这很难在真实的PC机上做到.

6.828课程中使用QEMU仿真器, 一种现代的和相对快速的仿真器. 而QEMU内置的监视模式提供了有限的调试支持. QEMU可以作为GNU debugger(GDB)操作的一个远程调试目标. 在该实验中将利用它们逐步调试早期的启动过程.

首先,下载实验代码
> $ git clone https://pdos.csail.mit.edu/6.828/2014/jos.git lab


然后在当前实验目录中编译代码,构建最小的6.828 boot loader和kernel
> $ make

```
fatansy@fantasy:~/my_dev/mit-os/mit-jos-2014/Lab1/2014-jos-Lab1$ make 
+ as kern/entry.S 
+ cc kern/entrypgdir.c 
+ cc kern/init.c 
+ cc kern/console.c 
+ cc kern/monitor.c 
+ cc kern/printf.c 
+ cc kern/kdebug.c 
+ cc lib/printfmt.c 
+ cc lib/readline.c 
+ cc lib/string.c 
+ ld obj/kern/kernel 
+ as boot/boot.S 
+ cc -Os boot/main.c 
+ ld boot/boot 
boot block is 392 bytes (max 510) 
+ mk obj/kern/kernel.img 
```

最后开始运行QEMU, 提供文件obj/kern/kernel.img(由make命令创建). 作为仿真的PC的”虚拟硬盘”的内容, 该硬盘镜像包含boot loader(obj/boot/boot)和内核(obj/kernel).
> $ make qemu


## 2.3 PC的物理地址空间

# 第2部分 Boot Loader
------
PC上软盘和硬盘分为512字节的区域被称为sectors. 一个sector是磁盘最小的传输粒度:每次的读或者写操作必须时一个或多个sectors且以一个sector边界对齐.

若磁盘是启动盘,则第一个sector称为boot sector,因为该sector中存放的是boot loader代码. 
当BIOS找到可启动的软盘或者硬盘, BIOS加载512字节的boot sector到内存的物理地址0x7C00到0x7dff处, 然后使用jmp指令设置CS:IP为0x0000:0x7C00, 把控制权交给boot loader程序. 跟BIOS的加载地址奕扬,这些地址可以是任意的 –-- 但是对于PC来说,这些地址是固定的和标准化的.

从CD-ROM启动的能力在PC的发展过程中来的非常的迟, 结果PC架构利用该机会重新考虑启动流程. 结果现代BIOS从CD-ROM启动的方式变得有点复杂(也更强大). 
CD-ROMs使用sector大小为2048字节来代替512字节. 同时BIOS在把控制权交给boot load之前可以从磁盘加载更加大的boot image到内存(不仅仅一个sector). 更多信息,参考:["El Torito" Bootable CD-ROM Format Specification](https://pdos.csail.mit.edu/6.828/2014/readings/boot-cdrom.pdf).


对于6.828课程,使用传统的硬盘启动机制, 意味着我们的boot loader必须放在仅有的512字节中. Boot loader程序由一个汇编源代码boot/boot.S和一个C源代码boot/main.c组成. 仔细阅读这些源代码, 确保理解这些代码的执行流程. 该boot loader必须执行两个功能:

1. 首先, boot loader把处理器的模式从实模式切换到32-bit保护模式, 因为只有在保护模式下软件才能访问处理器物理地址空间1MB以上的所有内存. 保护模式概念的阐述见[PC Assembly Language](https://pdos.csail.mit.edu/6.828/2014/readings/pcasm-book.pdf)中的1.2.7和1.2.8部分, 更加详细的细节见Intel架构手册.

2. 其次




# 第3部分 Kernel
------



# OTHERS
Linux下用./configure && make && make install 安装的软件,如何卸载? 

1)在安装软件的源代码中,找到makefile文件,看看其中有没有uninstall这一项.若有,则直接在源代码目录中输入make uninstall来卸载即可. 

2)若makefile文件中没有uninstall这一项,那么就需要手动删除安装的目录. 
那么如何知道安装的目录在哪里呢? 
这个就需要在安装软件时,记录下安装时的Log,如下命令: 
> $ make >& LOG_make &
 
> $ make install >& LOG_install &
