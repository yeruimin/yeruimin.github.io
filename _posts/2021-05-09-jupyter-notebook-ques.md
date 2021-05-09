---
title: Jupyter Notebook解决虚拟环境自动代码补全失灵问题
categories: [homework]
comments: true
---

## 问题

为了学习tensorflow和pytorch，在anaconda中创建了虚拟环境tensorflow2

在安装nbextensions（安装在base环境中）时发现在base环境下可以实现所有包中函数的代码补全，但是在tensorflow2环境中，可以实现import [包名] 的代码补全，但是调用包中函数时不显示补全。

## 解决：

先是按照教程更改kernel.json文件，创建两个kernel来区分tensorflow2和base，但是出现了新的问题。

在base环境中打开jupyter notebook中的tensorflow kernel会显示无法找到python.exe入口，因此，必须从tensorflow2的jupyter notebook中才能自由更改两个kernel。

同时，自动代码补全问题还是没有解决。python tensorflow kernel下还是无法实现代码自动补全。于是在环境tensorflow2下再安装一次nbextensions整个流程，就可以了。

## 现在的流程：
+ 进入jupyter notebook需要从jupyter notebook(tensorflow2)中进入，否则不能打开python tensorflow kernel。
