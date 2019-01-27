---
title: "Int"
layout: post
date: 2019-01-22 11:01
image: /assets/images/swift_logo.png
headerImage: true
tag:
- swift
star: false
category: blog
author: james
description: swift standard library
---
## Int(exactly:)
```swift
if let x = Int(exactly: 3.0) {
    print(x)
} else {
    print("return nil")
}
// prints "3"


if let x = Int(exactly: 3.14) {
    print(x)
} else {
    print("return nil")
}
// prints "return nil"

```

## random(in:)类方法

```swift
for _ in 1...3 {
    print(Int.random(in: 1..<100))
}


for _ in 1...3 {
    print(Int.random(in: 1...100))
}
```

## negate()方法

```swift
var a = 4
a.negate()
print(a)
// prints "-4"
```

## quotientAndRemainder(dividingBy:)商余数方法

```swift
var x = 100
let (quo, rem) = x.quotientAndRemainder(dividingBy: 16)
print("商是：\(quo)，余数是：\(rem)。")
// prints "商是：6，余数是：4。"
```

## abs(_:)方法

```swift
let x = -34
let y = abs(x)
print(y)
```

## signum()方法 
负数返回-1，正数返回1，其它，返回0。

## decription属性
`3.decription`

## customMirror属性
??
