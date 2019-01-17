---
title: "字符串和字符"
layout: post
date: 2019-01-16 14:01
image: /assets/images/swift_logo.png
headerImage: true
tag:
- swift
star: false
category: blog
author: james
description: learning swift
---

## 字符串和字符  
### 字符字面量
✯ 要让多行字符串字面量开始或结束带有换行，写一个空行作为第一行或者是最后一行。比如：
  
```  
"""
  
This string starts with a line feed.  
It also ends with a line feed.  

"""  
```

多行字符串可以缩进以匹配周围的代码。三引号（ """ ）前的空格会告诉 Swift 其他行前应该有多少空白是需要忽略的。如果你在某行的空格超过了结束的三引号（ """ ），那么这些空格会被包含。

### 操作字符
String值可以通过传入 Character值的字符串作为实际参数到它的初始化器来构造：

```
1 let catCharacters: [Character] = ["C", "a", "t", "!", "?"] ////必须声明类型
2 let catString = String(catCharacters)
3 print(catString)
4 // prints "Cat!?"
```

### 字符串索引
每一个 String值都有相关的索引类型， String.Index，它相当于每个 Character在字符串中的位置。  

使用 startIndex属性来访问 String中第一个 Character的位置。 endIndex属性就是 String中最后一个字符后的位置。
  
使用 index(before:) 和 index(after:) 方法来访问给定索引的前后。要访问给定索引更远的索引，你可以使用 index(_:offsetBy:) 方法而不是多次调用这两个方法。

```
 1 let greeting = "Guten Tag!"
 2 greeting[greeting.startIndex]
 3 // G
 4 greeting[greeting.index(before: greeting.endIndex)]
 5 // !
 6 greeting[greeting.index(after: greeting.startIndex)]
 7 // u
 8 let index = greeting.index(greeting.startIndex, offsetBy: 7)
 9 greeting[index]
10 // a
```

使用 indices属性来访问字符串中每个字符的索引。

```
1 for index in greeting.indices {
2     print("\(greeting[index]) ", terminator: "")
3 }
4 // Prints "G u t e n   T a g ! "
```

### 前缀和后缀相等性
要检查一个字符串是否拥有特定的字符串前缀或者后缀，调用字符串的 `hasPrefix(_:)`和 `hasSuffix(_:)`方法，它们两个都会接受一个 `String` 类型的实际参数并且返回一个布尔量值。
