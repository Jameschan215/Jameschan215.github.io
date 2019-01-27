---
title: "泛型（Generics）"
layout: post
date: 2019-01-21 19:49
image: /assets/images/swift_logo.png
headerImage: true
tag:
- swift
star: false
category: blog
author: james
description: learning swift
---
## 类型参数
类型参数指定并命名一个占位类型，并且紧随在函数名后面，使用一对尖括号括起来（例如` <T>`）。  

在大多数情况下，类型参数具有一个描述性名字(`Array<Element>`)，然而，当它们之间没有有意义的关系时，通常使用单个字母来命名，例如 T、U、V(`swapTwoValues<T>`)。

## 泛型类型
```swift
struct Stack<Element> {
    var items = [Element]()
    mutating func push(_ item: Element) {
        items.append(item)
    }
    mutating func pop() -> Element {
        return items.removeLast()
    }
}

----------------------------------------------

var stackOfStrings = Stack<String>()
stackOfStrings.push("uno")
stackOfStrings.push("dos")
stackOfStrings.push("tres")
stackOfStrings.push("cuatro")
// 栈中现在有 4 个字符串
```
## 类型约束
类型约束可以指定一个类型参数必须继承自指定类，或者符合一个特定的协议或协议组合。
语法：

```swift
func someFunction<T: SomeClass, U: SomeProtocol>(someT: T, someU: U) {
    // 这里是泛型函数的函数体部分
}
```
`someClass`是必须继承的类，`someProtocol`是必须符合的协议。
例：

```swift
func findIndex<T: Equatable>(of valueToFind: T, in array:[T]) -> Int? {
    for (index, value) in array.enumerated() {
        if value == valueToFind {
            return index
        }
    }
    return nil
}
```

## 关联类型
关联类型为协议中的某个类型提供了一个占位名（或者说别名），其代表的实际类型在协议被采纳时才会被指定。你可以通过 `associatedtype` 关键字来指定关联类型。

```swift
protocol Container {
    associatedtype Item  // Item就是关联类型
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
}
```
```swift
struct IntStack: Container {
    // IntStack 的原始实现部分
    var items = [Int]()
    mutating func push(_ item: Int) {
        items.append(item)
    }
    mutating func pop() -> Int {
        return items.removeLast()
    }
    // Container 协议的实现部分
    
    typealias Item = Int    // 确定了关联类型的类型为Int
    
    mutating func append(_ item: Int) {
        self.push(item)
    }
    var count: Int {
        return items.count
    }
    subscript(i: Int) -> Int {
        return items[i]
    }
}
```
## 通过扩展一个存在的类型来指定关联类型
`extension Array: Container {}`

## 给关联类型添加约束

```swift
protocol Container {
    associatedtype Item: Equatable  //能过协议约束
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
}
```

## 在关联类型约束里使用协议

```swift
protocol SuffixableContainer: Container {
    associatedtype Suffix: SuffixableContainer where Suffix.Item == Item
    func suffix(_ size: Int) -> Suffix
}
```
关联类型`Suffix` 拥有两个约束：它必须遵循 SuffixableContainer 协议，以及它的 Item 类型必须是和容器里的 Item 类型相同。

