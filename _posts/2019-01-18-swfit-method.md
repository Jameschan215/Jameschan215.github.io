---
title: "方法"
layout: post
date: 2019-01-18 15:09
image: /assets/images/swift_logo.png
headerImage: true
tag:
- swift
star: false
category: blog
author: james
description: learning swift
---

## 实例方法
### 在mutating方法里指定自身
异变方法可以指定整个实例给隐含的 self属性。

```swift
struct Point {
    var x = 0.0, y = 0.0
    mutating func moveBy(x deltaX: Double, y deltaY: Double) {
        self = Point(x: x + deltaX, y: y + deltaY)
    }
}
```

枚举的异变方法可以把隐含的 self属性设置为相同枚举里的不同成员(case)：  
Mutating methods for enumerations can set the implicit self parameter to be a different case from the same enumeration:

```swift
enum TriStateSwitch {
    case off, low, high
    mutating func next() {
        switch self {
        case .off:
            self = .low
        case .low:
            self = .high
        case .high:
            self = .off
        }
    }
}
var ovenLight = TriStateSwitch.low
ovenLight.next()
// ovenLight is now equal to .high
ovenLight.next()
// ovenLight is now equal to .off
```

## 类型方法
在 `func`关键字之前使用 `static`关键字来明确一个类型方法。类同样可以使用 `class`关键字来允许子类重写父类对类型方法的实现。
