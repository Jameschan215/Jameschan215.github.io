---
title: "集合类型"
layout: post
date: 2019-01-17 10:25
image: /assets/images/swift_logo.png
headerImage: true
tag:
- swift
star: false
category: blog
author: james
description: learning swift
---

## 集合类型 
### 集合的可变性
如果你把数组、合集或者字典赋值给一个常量，则集合就成了不可变的，它的**大小和内容**都不能被改变。

### 数组

数组可以相加（+）：

```swift
1 var anotherThreeDoubles = Array(repeating: 2.5, count: 3)
2 // anotherThreeDoubles is of type [Double], and equals [2.5, 2.5, 2.5]
 
3 var sixDoubles = threeDoubles + anotherThreeDoubles
4 // sixDoubles is inferred as [Double], and equals [0.0, 0.0, 0.0, 2.5, 2.5, 2.5]
```

另外，可以使用加赋值运算符 ( +=)来在数组末尾添加一个或者多个同类型元素：

```swift
1 shoppingList += ["Baking Powder"]
2 // shoppingList now contains 4 items
3 shoppingList += ["Chocolate Spread", "Cheese", "Butter"]
4 // shoppingList now contains 7 items
```

你同样可以使用下标脚本语法来一次改变一个范围的值，就算替换与范围长度不同的值的合集也行。下面的栗子替换用 "Bananas"和 "Apples"替换 "Chocolate Spread", "Cheese", and "Butter"：

```swift
1 shoppingList[4...6] = ["Bananas", "Apples"]
2 // shoppingList now contains 6 items
```

★ 请研究一下swift标准库里Array的具体属性和方法，点击*[这里](https://developer.apple.com/documentation/swift/array)*。

### 集合
合集（set）是无序的，值不重复的。

#### Set类型的哈希值
合集中的类型必须是可哈希的。

所有 Swift 的基础类型（比如 `String`, `Int`, `Double`, 和 `Bool`）默认都是可哈希的，并且可以用于合集或者字典的键。没有关联值的枚举成员值（如同枚举当中描述的那样）同样默认可哈希。

★ 自定义类型作为合集的值类型或者字典的键类型时，必须让它们遵循`Hashable`协议。遵循 Hashable协议的类型必须提供可获取的叫做 hashValue的 Int属性。因为 Hashable协议遵循 Equatable，遵循的类型必须同时一个“等于”运算符 ( ==)的实现。

#### 使用数组字面量创建合集
合集类型不能从数组字面量推断出来，所以 `Set`类型必须被显式地声明。但是可以推断集合值的类型，下例可以把`Set<String>`中尖括号部分的内容去掉：

`var favoriteGenres: Set = ["Rock", "Classical", "Hip hop"]`

可以通过调用合集的 `remove(_:)`方法来从合集当中移除一个元素，如果元素是合集的成员就移除它，并且返回移除的值，如果合集没有这个成员就返回 nil。另外，合集当中所有的元素可以用 removeAll()一次移除。

要检查合集是否包含了特定的元素，使用 `contains(_:)`方法。

#### 合集成员关系和相等性
* 使用“相等”运算符 ( == )来判断两个合集是否包含有相同的值；
* 使用 isSubset(of:) 方法来确定一个合集的所有值是被某合集包含；
* 使用 isSuperset(of:)方法来确定一个合集是否包含某个合集的所有值；
* 使用 isStrictSubset(of:) 或者 isStrictSuperset(of:)方法来确定是个合集是否为某一个合集的子集或者超集，但并不相等；
* 使用 isDisjoint(with:)方法来判断两个合集是否拥有完全不同的值。


### 字典

1. 可以用下标脚本给字典添加新元素。 `airports["LHR"] = "London"`
2. 使用字典的 `updateValue(_:forKey:)`方法来设置或者更新键的值，并返回旧值，并且该返回值是可选的。
3. 下标脚本语法来从字典的特点键中取回的值也是可选的，因为存在键没有值的情况。
4. 使用下标脚本语法给一个键赋值 nil，来从字典当中移除一个键值对，即`key`和`value`全被删除了。
5. 使用 removeValue(forKey:)来从字典里移除键值对。如果存在键、值，移除并且返回移除的值，如果值不存在则返回 nil：

``` swift
if let removedValue = airports.removeValue(forKey: "DUB") {
    print("The removed airport's name is \(removedValue).")
} else {
    print("The airports dictionary does not contain a value for DUB.")
}
// Prints "The removed airport's name is Dublin Airport."
```

#### 遍历字典
用 for-in循环来遍历字典的键值对，也可以通过访问字典的 keys和 values属性来取回可遍历的字典的键或值的集合：

```swift
for (airportCode, airportName) in airports {
    print("\(airportCode): \(airportName)")
}
// YYZ: Toronto Pearson
// LHR: London Heathrow
```

```swift
for airportCode in airports.keys {
    print("Airport code: \(airportCode)")
}
// Airport code: YYZ
// Airport code: LHR
 
for airportName in airports.values {
    print("Airport name: \(airportName)")
}
// Airport name: Toronto Pearson
// Airport name: London Heathrow
```