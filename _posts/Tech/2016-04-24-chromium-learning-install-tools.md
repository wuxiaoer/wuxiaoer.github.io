---
layout: post
title: chromium学习之工具安装 
category: Tech 
tags: 
    - chromium
keywords: chromium, depot_tools
description:
---

## Linux下安装depot_tools

Chromium和Chromium OS使用depot_tools的脚本管理包来管理 checkout和code reviews

depot_tools工具包包含: gclient, gcl, git-cl, repo等

1. 确保git已经安装
2. 获取depot_tools:

```
$ git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git
```

3. 添加depot_tools路径到系统PATH中
$ export PATH=`pwd`/depot_tools:"$PATH"

## Linux下chromium代码下载

下载chromium代码的操作流程参考:

[Get the Code: Checkout, Build, Run & Submit](https://www.chromium.org/developers/how-tos/get-the-code)

## 参考:
 - [Install depot_tools](http://www.chromium.org/developers/how-tos/install-depot-tools)

