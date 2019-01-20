---
title: "错误处理"
layout: post
date: 2019-01-20 14:14
image: /assets/images/swift_logo.png
headerImage: true
tag:
- swift
star: false
category: blog
author: james
description: learning swift
---
## 处理错误
在 Swift 中有四种方式来处理错误：

1. 你可以将来自函数的错误传递给调用函数的代码中；
2. 使用 do-catch 语句来处理错误；
3. 把错误作为可选项的值；
4. 或者错误不会发生的断言。

## 使用 Do-Catch 处理错误
下面是`do-catch`语句的常用形式：

```swift
do {
    try expression
    statements
} catch pattern 1 {
    statements
} catch pattern 2 where condition {
    statements
} catch {
    statements
}
```

例：

```swift
var vendingMachine = VendingMachine()
vendingMachine.coinsDeposited = 8
do {
    try buyFavoriteSnack("Alice", vendingMachine: vendingMachine)
    // Enjoy delicious snack
} catch VendingMachineError.invalidSelection {
    print("Invalid Selection.")
} catch VendingMachineError.outOfStock {
    print("Out of Stock.")
} catch VendingMachineError.insufficientFunds(let coinsNeeded) {
// coinsNeeded 是 .nsufficientFunds 的关联值
    print("Insufficient funds. Please insert an additional \(coinsNeeded) coins.")
}
// prints "Insufficient funds. Please insert an additional 2 coins."
```
1. 在不抛出错误的函数中， do-catch 分句就必须处理错误。
2. 在可抛出函数中，要么 do-catch 分句处理错误，要么调用者处理。
3. 如果错误被传递到了顶层生效范围但还是没有被处理，你就会得到一个运行时错误了。

## 指定清理操作
`defer` 语句将代码的执行延迟到当前的作用域退出之前。该语句由 `defer` 关键字和要被延迟执行的语句组成。延迟执行的语句不能包含任何控制转移语句，例如 `break`、`return` 语句，或是抛出一个错误。延迟执行的操作会按照它们声明的顺序从后往前执行——也就是说，第一条 `defer` 语句中的代码最后才执行，第二条 `defer` 语句中的代码倒数第二个执行，以此类推。最后一条语句会第一个执行。

```swift
func processFile(filename: String) throws {
    if exists(filename) {
        let file = open(filename)
        defer {
            close(file)
        }
        while let line = try file.readline() {
            // 处理文件。
        }
        // close(file) 会在这里被调用，即作用域的最后。
    }
}
```

上面的代码使用一条 defer 语句来确保 `open(_:)` 函数总是有一个相应的对 `close(_:)` 函数的调用。  

★ 即使没有涉及到错误处理的代码，你也可以使用 defer 语句。
