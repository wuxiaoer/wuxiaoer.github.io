---
layout: post
title: MIT OS课程之Qemu安装
category: Tech
tags: os
keywords: mit, os
description:
---

# QEMU Emulator安装 
------

QEMU是一个现代的,快速的PC仿真器, QEMU-1.7.0用于操作系统开发.

然而, QEMU的调试功能非常的不成熟, 因此在用QEMU调试操作系统开发中, 推荐使用MIT提供的QEMU patch版本.

版本的下载地址:
git clone https://github.com/geofft/qemu.git -b 6.828-1.7.0

在Linux系统上安装时, 需要安装SDL开发库 以获得图形VGA窗口, 在Debian/Ubuntu, 即安装libsdl1.2-dev包



下载完qemu patch版本, 按如下流程安装
> 1. 配置
> $./configure --disable-kvm [--prefix=PFX] [--target-list="i386-softmmu x86_64-softmmu"]
>
> 2. 编译
> $make
>
> 3. 安装
> $sudo make install
