---
title: 可视化电脑处理变量赋值、循环、程序运行的过程
author: ct
layout: post
categories:
  - Python
tags:
  - Bioinfo
---

[`Python Tutor`](http://www.pythontutor.com/)是`Philip Guo`开发的，通过把计算机运行程序代码的过程可视化的展示来帮助克服程序学习最初的障碍。

这款线上工具支持`Python 2`, `Python 3`, `Java`, `JavaScript`,  `TypeScript`, `Ruby`, `C`和`C++`代码。累计有多于180个国家三百五十万多人次使用。通过它可视化运行的代码有三千万之多。

下面的动图展示了一段Python程序的变量赋值，变量交换，列表赋值，列表增删，循环，判断，全局变量在运行时发生的动态变化，方便更好地理解。

![](http://www.ehbio.com/ehbio_resource/pythontutor2.gif)

```python
# 变量赋值
a = 1
b = 2

# 变量交换
a, b = b, a

# 列表赋值
c = [1, 2, 3]

# 列表增员
c.append(4)

# 列表传址
d = c

# 同时变化
d.append(5)

# 列表传值
e = c[:]

# 单列表改变
e.remove(5)

# 字符串变量
f = 'ehbio'
g = '生信宝典'

# 字符串相加，开辟新内存空间
f = f + g

# 字符串合并推荐方式
i = ''.join([f,g])

# 循环过程和判断
for j in range(5):
    if(j==2):
        print(j)

# 句部变量
def func():
    a = 1
    print(a)

func()

# 全局变量
def func2():
    global a
    a += 1
    print(a)

func2()
print(a)
```

