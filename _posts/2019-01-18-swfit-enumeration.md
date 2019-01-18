---
title: "枚举"
layout: post
date: 2019-01-18 13:26
image: /assets/images/swift_logo.png
headerImage: true
tag:
- swift
star: false
category: blog
author: james
description: learning swift
---

## 遍历枚举情况（case） 
可以通过在枚举名字后面写 : CaseIterable 来允许枚举被遍历。Swift 会暴露一个包含对应枚举类型所有情况的集合名为 allCases 。

```swift
enum Beverage: CaseIterable {
    case coffee, tea, juice
}
let numberOfChoices = Beverage.allCases.count
print("\(numberOfChoices) beverages available")
// Prints "3 beverages available"

for beverage in Beverage.allCases {
    print(beverage)
}
// coffee
// tea
// juice
```

## 原始值
要想有原始值，必须在声明时明确类型。  
1. 字符`enum ASCIIControlCharacter: Character` 必须显式的指明原始值。如：`case tab = "\t"`  
2. 字符串 `enum CompassPoint: String ` 隐式的原始值即是成员值本身，如 `case north`的原始值就是`"north"`。  
3. 整数值 `enum CompassPoint: Int` 隐式的原始值是从0开始，可显式的指定起始数值。

## 从原始值初始化
这个初始化是可失败的，可nil。
```swift
let possiblePlanet = Planet(rawValue: 7)
// possiblePlanet is of type Planet? and equals Planet.Uranus
```

## 递归枚举
***递归枚举是拥有另一个枚举作为枚举成员关联值的枚举。***你可以在声明枚举成员之前使用 `indirect`关键字来明确它是递归的。

```swift
enum ArithmeticExpression {
    case number(Int)
    indirect case addition(ArithmeticExpression, ArithmeticExpression)
    indirect case multiplication(ArithmeticExpression, ArithmeticExpression)
}
```
所有成员可递归，如下：

```swift
indirect enum ArithmeticExpression {
    case number(Int)
    case addition(ArithmeticExpression, ArithmeticExpression)
    case multiplication(ArithmeticExpression, ArithmeticExpression)
}
```
 