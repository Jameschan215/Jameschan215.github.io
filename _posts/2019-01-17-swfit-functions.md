---
title: "函数"
layout: post
date: 2019-01-17 20:25
image: /assets/images/swift_logo.png
headerImage: true
tag:
- swift
star: false
category: blog
author: james
description: learning swift
---

## 函数
### 可变形式参数
一个可变形式参数可以接受零或者多个特定类型的值，可以通过在形式参数的类型名称后边插入三个点符号（ ...）来书写可变形式参数。

```swift
func arithmeticMean(_ numbers: Double...) -> Double {
    var total: Double = 0
    for number in numbers {
        total += number
    }
    return total / Double(numbers.count)
}
arithmeticMean(1, 2, 3, 4, 5)
// returns 3.0, which is the arithmetic mean of these five numbers
arithmeticMean(3, 8.25, 18.75)
// returns 10.0, which is the arithmetic mean of these three numbers
```

一个函数最多只能有一个可变形式参数。

### 输入输出形式参数
```swift
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}

var someInt = 3
var anotherInt = 107
swapTwoInts(&someInt, &anotherInt)
print("someInt is now \(someInt), and anotherInt is now \(anotherInt)")
// prints "someInt is now 107, and anotherInt is now 3"

```

用`inout`关键字可以定义一个输入输出形式参数，在调用函数时在参数前面添加（`&`）来明确参数可以被函数修改。
