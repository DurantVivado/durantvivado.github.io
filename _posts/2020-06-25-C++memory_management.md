---
layout:     post
title:      "C++内存管理"
subtitle:   " \"C++ Memory management\""
date:       2020-06-25 13:23:45
author:     "Durant"
latex: true
header-img: "img/post-bg-o.jpg"
catalog: true
tags:
   - C++
---





# C++内存管理

> 内存管理是非常让人头疼的事情，因为一不小心就可能导致内存泄漏，为此很多C++程序员跑路到java或python，？？？但是反过来说，优秀的程序员知道如何管理内存，并显式获得速度的飞跃。

内存分类：

1. **静态内存**：用来保存局部`static`对象，类的`static`数据成员以及定义在任何函数之外的变量。

2. **栈内存**：用来保存定义在函数内的非`static`对象。

   分配在静态或栈内存中的对象由编译器自动创建和销毁。

3. **动态内存**，又被称为**堆**(heap)，由程序的生命周期所控制，我们的代码必须*显式*的销毁它们。

通常我们用`new`创建一个对象，然后用`delete`销毁它。

> 提示：在<memory>头文件下

新的标准库，提供了两种智能指针：`shared_ptr`允许多个指针指向同一个对象。`unique`则”独占“所指向的对象。`weak_ptr`是一种弱引用，指向`shared_ptr`所指向的对象。

好的，下面讲讲怎么使用：

```C++
shared_ptr<string> p1;//必须指明对象
```

此外 p1还可以用于条件判断。

若要解引用对象，需要写成`(*p1)`