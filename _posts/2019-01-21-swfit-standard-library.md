---
title: "Swift Standard Library"
layout: post
date: 2019-01-22 18:40
image: /assets/images/swift_logo.png
headerImage: true
tag:
- swift
star: false
category: blog
author: james
description: swift standard library
---
## 全局函数
1. min()
2. max()
3. abs()

## String
### 方法
#### replaceSubrange(_:with:)
例一：

```swift
var nums = [10, 20, 30, 40, 50]
 nums.replaceSubrange(1...3, with: repeatElement(1, count: 5))
 print(nums)
 // Prints "[10, 1, 1, 1, 1, 1, 50]"
 ```
 
 例二：

 ```swift
 var str = "James Chen"
if let firstSpace = str.firstIndex(of: " ") {
    str.replaceSubrange(str.startIndex..<firstSpace, with: "Frank")
}
// Now str is "Frank Chen" 

```

#### removeAll(where:)
移除所有满足条件的元素，条件是一个闭包。
例一：

```swift
var name = "James David Beckham Chen"

name.removeAll { $0 == " "}
print(name)

// Prints "JamesDavidBeckhamChen"
```

例二：

```swift
var arr = ["C", "D", "F", "D", "G"]
arr.removeAll{ $0 == "D"}
print(arr)

// Prints "["C", "F", "G"]"
```

#### filter(_:)
例：

```swift
let cast = ["Vivien", "Marlon", "Kim", "Karl"]
let shortNames = cast.filter { $0.count < 5 }
print(shortNames)
// Prints "["Kim", "Karl"]"
```

#### drop(while:)
从头开始按顺序，当第一个字符满足条件时，drop它，否则不drop。

#### `dropLast(_:)`,  `dropLast(_ k: Int)`
drop最后一个，drop从后往前的k个元素。

#### lowercased() uppercased()
`print(name.lowercased())`

#### func split(separator: Character, maxSplits: Int = default, omittingEmptySubsequences: Bool = default) -> [Substring]

```swift
let line = "BLANCHE:   I don't want realism. I want magic!"
print(line.split(separator: " "))
// Prints "["BLANCHE:", "I", "don\'t", "want", "realism.", "I", "want", "magic!"]"

print(line.split(separator: " ", maxSplits: 1))
// Prints "["BLANCHE:", "  I don\'t want realism. I want magic!"]"

print(line.split(separator: " ", omittingEmptySubsequences: false))
// Prints "["BLANCHE:", "", "", "I", "don\'t", "want", "realism.", "I", "want", "magic!"]"
```


#### randomElement()
当数组为空时，返回nil。

```swift
let names = ["Zoey", "Chloe", "Amani", "Amaia"]
let randomName = names.randomElement()!
// randomName == "Amani"
```

#### map(_:)

```swift
let cast = ["Vivien", "Marlon", "Kim", "Karl"]
let lowercaseNames = cast.map { $0.lowercased() }
// 'lowercaseNames' == ["vivien", "marlon", "kim", "karl"]
let letterCounts = cast.map { $0.count }
// 'letterCounts' == [6, 6, 3, 4]
```
compactMap(_:)，无nil，非可选

```swift
let possibleNumbers = ["1", "2", "three", "///4///", "5"]

let mapped: [Int?] = possibleNumbers.map { str in Int(str) }
// [1, 2, nil, nil, 5]

let compactMapped: [Int] = possibleNumbers.compactMap { str in Int(str) }
// [1, 2, 5]
```

#### reduce(into:_:)

```swift
let letters = "abracadabra"
let letterCount = letters.reduce(into: [:]) { result, char in
    result[char, default: 0] += 1
}
// letterCount == ["a": 5, "b": 2, "r": 2, "c": 1, "d": 1]
```

遍历letters字符串，第一轮，result["a"] = 0 + 1 = 1，即result为 ["a": 1]   
                           第二轮，result["b"] = 0 + 1 = 1， 即result为 ["a": 1, "b": 1]  
                           第三轮，result["r"] = 0 + 1 = 1，即result为  ["a": 1, "b": 1, "r": 1]    
                           第四轮，result["a"] = 1 + 1 = 2，即result为  ["a": 2, "b": 1, "r": 1]  
                           ……  
                           最后，返回result，即 ["c": 1, "r": 2, "d": 1, "b": 2, "a": 5]
                           
         
#### forEach(_:)

```swift
let numberWords = ["one", "two", "three"]
for word in numberWords {
    print(word)
}
// Prints "one"
// Prints "two"
// Prints "three"

numberWords.forEach { word in
    print(word)
}
// Same as above
```
 

## Dictionary

任何遵循Hashable协议的类型都可以用作字典的key，包括所有的基础类型。自定义类型只要遵循Hashable协议也可以成为字典的Key。
