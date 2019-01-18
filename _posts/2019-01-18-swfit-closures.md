---
title: "闭包"
layout: post
date: 2019-01-18 12:44
image: /assets/images/swift_logo.png
headerImage: true
tag:
- swift
star: false
category: blog
author: james
description: learning swift
---

## 闭包要点  
### 例一：
 
```swift
let names = ["Chris","Alex","Ewa","Barry","Daniella"]

func backward(s1: String, s2: String) -> Bool {
    return s1 > s2
}

// 1
//let reversedNames = names.sorted(by: backward)

// 2 闭包
// let reversedNames = names.sorted(by: {(s1: String, s2: String) -> Bool in
//     return s1 < s2
// })

// 3 闭包，类型推断
// let reversedNames = names.sorted(by: {s1, s2 in return s1 > s2})

// 4 单表达式闭包隐式返回
// let reversedNames = names.sorted(by: {s1, s2 in s1 < s2})

// 5 简写实际参数名
// let reversedNames = names.sorted(by: { $0 > $1 })

// 6 运算符函数
//let reversedNames = names.sorted(by: < )

// 7 尾随闭包，省略参数标签 `by:`
// let reversedNames = names.sorted(){$0 > $1}

// 8 闭包是函数的唯一实际参数，可以省略()
let reversedNames = names.sorted{ $0 < $1 }

print(reversedNames)
```

### 自动闭包
自动闭包是自动创建的，包装了一个表达式的，被当作参数传入一个函数的东西。它不带参数，返回的是它所包装的表达式的值。语法是可以省略包围在函数参数外的括号，只需要写一个正常的表达式即可。  

自动闭包允许延迟处理，因为闭包内部的代码直到你调用它的时候才会运行。

```swift
var customersInLine = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
print(customersInLine.count)
// Prints "5"
 
let customerProvider = { customersInLine.remove(at: 0) }
print(customersInLine.count)
// Prints "5"
 
print("Now serving \(customerProvider())!")
// Prints "Now serving Chris!"
print(customersInLine.count)
// Prints "4"
```

**注意 `customerProvider` 的类型不是 `String` 而是 `() -> String` ——一个不接受实际参数并且返回一个字符串的函数。**

不使用明确的闭包时，可以通过 `@autoclosure` 标志标记它的形式参数使用了自动闭包。
