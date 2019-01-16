---
title: "基础内容"
layout: post
date: 2019-01-16 14:01
image: /assets/images/swift_logo.png
headerImage: true
tag:
- swift
star: true
category: blog
author: james
description: learning swift
---

## 基础内容  
### 输出常量和变量  
`print(_:separator:terminator:)`默认在行末添加换行符结束输出，若不想换行，就传入空的换行符作为结束，例：`print(someValue, terminator: "")`。  
  
### 数值型字面量  
* 一个十进制数，没有前缀  
* 一个二进制数，前缀是 0b  
* 一个八进制数，前缀是 0o
* 一个十六进制数，前缀是 0x  
  
十进制娄与 exp 的指数，结果就等于基数乘以10<sup>exp</sup>:   
  
* 1.25e2 意味着 1.25 x 102, 或者 125.0   
* 1.25e-2  意味着 1.25 x 10-2, 或者 0.0125  

  
整数和浮点数都可以添加额外的零或者添加下划线来增加代码的可读性。下面的这些格式都不会影响字面量的值：
      
>  
1.  `let paddedDouble = 000123.456`
2.  `let oneMillion = 1_000_000`
3.  `let justOverOneMillion = 1_000_000.000_000_1`
  
  
### 整数和浮点数转换 
在用浮点数初始化一个新的整数类型的时候，数值会被截断。也就是说 `4.75` 会变成 `4`， `-3.9` 会变为 `-3` 。   

### 类型别名  
**类型别名**可以为已经存在的类型定义了一个新的可选名字。用 typealias 关键字定义类型别名。   
> 1. `typealias AudioSample = UInt16`
> 2. `var maxAmplitudeFound = AudioSample.min`
