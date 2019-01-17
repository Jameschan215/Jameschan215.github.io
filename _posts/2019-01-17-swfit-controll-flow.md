---
title: "控制流"
layout: post
date: 2019-01-17 16:50
image: /assets/images/swift_logo.png
headerImage: true
tag:
- swift
star: false
category: blog
author: james
description: learning swift
---

## 控制流
### For-in 循环
```swift
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}
``` 

上例中`index`是一个常量，但不需要用`let`显式的写出。

如果你不需要序列的每一个值，你可以使用下划线来取代遍历名以忽略值。`for _ in 1...power {}`

半开区间`stride(from:to:by:)` 函数用法：

```swift
let minuteInterval = 5
for tickMark in stride(from: 0, to: minutes, by: minuteInterval) {
    // render the tick mark every 5 minutes (0, 5, 10, 15 ... 45, 50, 55)
}
```

闭区间`stride(from:through:by:)`函数用法：

```swift
let hours = 12
let hourInterval = 3
for tickMark in stride(from: 3, through: hours, by: hourInterval) {
    // render the tick mark every 3 hours (3, 6, 9, 12)，如果用to，则输出是(3, 6, 9)
}
```

### Switch
#### 区间匹配
switch情况的值可以在一个区间中匹配：

```swift
let approximateCount = 62
let countedThings = "moons orbiting Saturn"
var naturalCount: String
switch approximateCount {
case 0:
    naturalCount = "no"
case 1..<5:
    naturalCount = "a few"
case 5..<12:
    naturalCount = "several"
case 12..<100:
    naturalCount = "dozens of"
case 100..<1000:
    naturalCount = "hundreds of"
default:
    naturalCount = "many"
}
print("There are \(naturalCount) \(countedThings).")
// prints "There are dozens of moons orbiting Saturn."
```

#### 元组
你可以使用元组来在一个 switch 语句中测试多个值。每个元组中的元素都可以与不同的值或者区间进行匹配。另外，使用下划线（ _）来表明匹配所有可能的值。

```swift
let somePoint = (1, 1)
switch somePoint {
case (0, 0):
    print("(0, 0) is at the origin")
case (_, 0):
    print("(\(somePoint.0), 0) is on the x-axis")
case (0, _):
    print("(0, \(somePoint.1)) is on the y-axis")
case (-2...2, -2...2):
    print("(\(somePoint.0), \(somePoint.1)) is inside the box")
default:
    print("(\(somePoint.0), \(somePoint.1)) is outside of the box")
}
// prints "(1, 1) is inside the box"
```

#### 值绑定
switch 情况可以将匹配到的值临时绑定为一个常量或者变量，来给情况的函数体使用。

```swift
let anotherPoint = (2, 0)
switch anotherPoint {
case (let x, 0):
    print("on the x-axis with an x value of \(x)")
case (0, let y):
    print("on the y-axis with a y value of \(y)")
case let (x, y):
    print("somewhere else at (\(x), \(y))")
}
// prints "on the x-axis with an x value of 2"
```

#### Where
switch 情况可以使用 where 分句来检查额外的情况，使用 where 分句，来创建动态过滤， switch 情况只有 where 分句情况评定等于 true 时才会匹配这个值。

```swift
let yetAnotherPoint = (1, -1)
switch yetAnotherPoint {
case let (x, y) where x == y:
    print("(\(x), \(y)) is on the line x == y")
case let (x, y) where x == -y:
    print("(\(x), \(y)) is on the line x == -y")
case let (x, y):
    print("(\(x), \(y)) is just some arbitrary point")
}
// prints "(1, -1) is on the line x == -y"
```

#### Fallthrough
switch 语句会在第一个匹配到的情况执行完毕之后就直接结束执行，fallthrough 关键字则是使代码执行直接移动到下一个情况（或者 default 情况）的代码块中。


#### 给语句打标签

```swift
gameLoop: while square != finalSquare {
    diceRoll += 1
    if diceRoll == 7 { diceRoll = 1 }
    switch square + diceRoll {
    case finalSquare:
        // diceRoll will move us to the final square, so the game is over
        break gameLoop
    case let newSquare where newSquare > finalSquare:
        // diceRoll will move us beyond the final square, so roll again
        continue gameLoop
    default:
        // this is a valid move, so find out its effect
        square += diceRoll
        square += board[square]
    }
}
print("Game over!")
```

#### 检查API的可用性
```swift
if #available(iOS 10, macOS 10.12, *) {
    // Use iOS 10 APIs on iOS, and use macOS 10.12 APIs on macOS
} else {
    // Fall back to earlier iOS and macOS APIs
}
```

上边的可用性条件确定了在 iOS 平台， if 函数体只在 iOS 10 及以上版本才会执行；对于 macOS 平台，在只有在 macOS 10.12 及以上版本才会运行。最后一个实际参数， * ，它需求并表明在其他所有平台， if 函数体执行你在目标里明确的最小部属。