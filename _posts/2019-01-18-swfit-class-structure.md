---
title: "类和结构体"
layout: post
date: 2019-01-18 14:36
image: /assets/images/swift_logo.png
headerImage: true
tag:
- swift
star: false
category: blog
author: james
description: learning swift
---

## 特征运算符
利用恒等运算符来检查两个常量或者变量是否引用相同的实例：  

*  相同于   `(===)`
*  不相同于`(!==)`    

* “相同于”意味着两个类类型常量或者变量引用自相同的实例；
* “等于”意味着两个实例的在值上被视作“相等”或者“等价”

## 字符串，数组和字典的赋值与拷贝行为
Swift 的 String , Array 和 Dictionary类型是作为结构体来实现的，而基础库中的 NSString, NSArray和 NSDictionary，它们是作为类来实现的，而不是结构体。 NSString , NSArray 和 NSDictionary实例总是作为一个已存在实例的引用而不是拷贝来赋值和传递。
