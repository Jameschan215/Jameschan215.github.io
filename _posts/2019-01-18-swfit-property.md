---
title: "属性"
layout: post
date: 2019-01-18 14:55
image: /assets/images/swift_logo.png
headerImage: true
tag:
- swift
star: false
category: blog
author: james
description: learning swift
---

## 存储属性
### 常量结构体实例的存储属性
如果你创建了一个结构体的实例并且把这个实例赋给**常量**，你不能修改这个实例的属性，即使是声明为变量的属性。
## 类型属性
1. 必须总是给存储类型属性一个默认值，这是因为类型本身不能拥有能够在初始化时给存储类型属性赋值的初始化器。
2. 存储类型属性是在它们第一次访问时延迟初始化的。它们保证只会初始化一次，就算被多个线程同时访问，他们也不需要使用 lazy 修饰符标记。
