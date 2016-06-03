---
published: true
layout: post
title: VIM阅读源代码常用命令 
category: Tech 
tags: 
  - vim 
time: 2016.03.13 14:22:00
excerpt: NULL

---

### "[["和"]]"
```
[[: 跳转到当前光标所在位置的函数头
]]: 跳转到当前光标所在位置的函数尾
```

### 创建/打开/保存文件:
```
:new file.extension  --- 新建文件
:e file              --- 打开文件
:w file              --- 保存文件
:wq                  --- 保存退出
:x                   --- 退出, 如果文件已修改则保存
```
### 删除操作
```
dw  --- 删除光标之后的单词剩余部分。
d$  --- 删除光标之后的该行剩余部分。
dd  --- 删除当前行。

c   --- 功能和d相同，区别在于完成删除操作后进入INSERT MODE
cc  --- 也是删除当前行，然后进入INSERT MODE
```

### 翻页操作
```
ctrl + d    --- 向下翻半页（d:down)
ctrl + u    --- 向上翻半页 (u:up)

ctrl + f    --- 向下翻正页 (f:forward)
ctrl + b    --- 向上翻正页 (b:backward)
```

### 当前文本中插入时间
```
:r!date
```

### 参考文档
- [yavide: modern C C++ IDE over vim(经典的把VIM改造为IDE工具)](http://tuxdiary.com/2015/02/15/yavide/)
