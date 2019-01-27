---
title: "继承 Inheritance"
layout: post
date: 2019-01-18 19:10
image: /assets/images/swift_logo.png
headerImage: true
tag:
- swift
star: false
category: blog
author: james
description: learning swift
---

## 重写属性 
### 重写属性的GETTER和SETTER
你可以提供一个自定义的Getter(和Setter，如果合适的话)来重写任意继承的属性，无论在最开始继承的属性实现为储属性还是计算属性。必须声明你重写的属性名字和类型。子类可以把继承来的父类的只读属性重写成可读写的属性，但***不能把继承来的读写属性重写为只读属性。*** 

*如果你提供了一个setter作为属性重写的一部分，你也就必须为重写提供一个getter。如果你不想在重写getter时修改继承属性的值，那么你可以简单通过从getter返回 super.someProperty 来传递继承的值。*

### 重写属性观察器
* 不能给继承而来的常量存储属性或者只读的计算属性添加属性观察器，这些属性的值不能被设置。
* 不能为同一个属性同时提供重写的setter和重写的属性观察器，因为setter也可以监听。

## 阻止重写
在`class`关键字前写`final`可以将整个类标记为不可继承。

