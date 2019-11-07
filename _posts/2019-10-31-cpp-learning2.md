---
layout:     post
title:      cpp碎片学习
subtitle:   关键词
date:       2019-10-31
author:     Datoucai
header-img: img/guigui-title.jpg
catalog: true
tags:
    - cpp

---

## 关键词学习

### expilcit
在类的构造函数前， 禁止隐式的类型转换，规避风险

### inline关键词

inline是编译器的一种优化措施

当函数被声明为内联函数之后, 编译器会将其内联展开，

而不是按通常的函数调用机制进行调用.

调用函数有很多优点：可以复用，灵活性强，使用方便，代码简洁等等。

但是对于大多数机器而言， 调用函数的代价高于求解等价表达式。

而cpp中的inline关键词目的就是为了提高函数的执行效率

内联函数通常就是将它在程序中的每个调用点上“内联地”展开

tips：

- **inline**关键词必须放在**定义之前**而不是声明之前

因为用户没有必要也不需要知道一个函数是否需要内联

- inline是程序员的 **希望执行** 而不是强制执行



p = \softmax({pred})

    L = -\sum_i \log p_{i,{label}_i}