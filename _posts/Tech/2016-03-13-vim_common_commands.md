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

方法1：

```
:r!date
```

方法2：

使用<C-r>=来输入命令。可以在插入模式下，输入Ctrl+r,然后输入=号，之后输入如下命令：strftime("%Y-%m-%d %H:%M:%S")即可。 这样会在当前光标插入对应的时间

strftime后面的一串时间格式化符号很难记住，因此可以使用ab来缩写：使当我们在插入模式输入xtime时即可插入当前时间。
在.vimrc中添加上这一行：
iab xtime <c-r>=strftime("%Y-%m-%d %H:%M:%S")<cr>

### 参考文档
- [yavide: modern C C++ IDE over vim(经典的把VIM改造为IDE工具)](http://tuxdiary.com/2015/02/15/yavide/)


