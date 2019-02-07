---
title: "JSONEncoder&JSONDecoder"
layout: post
date: 2019-01-30 00:41
image: /assets/images/swift_logo.png
headerImage: true
tag:
- translate
star: false
category: blog
author: james
description: Foundation & translate
---
## JSONEncoder
An object that encodes instances of a data type as JSON objects.  
一个把实例的数据转换成JSON对象的对象。  

## Overview
下面的示例显示如何把一个简单的GroceryProduct类型的实例编码为JSON对象。 该类型遵循Codable协议，因此可以使用JSONEncoder实例将其编码为JSON。

```swift
struct GroceryProduct: Codable {
    var name: String
    var points: Int
    var description: String?
}

let pear = GroceryProduct(name: "Pear", points: 250, description: "A ripe pear.")

let encoder = JSONEncoder()
encoder.outputFormatting = .prettyPrinted

let data = try encoder.encode(pear)
print(String(data: data, encoding: .utf8)!)

/* Prints:
 {
   "name" : "Pear",
   "points" : 250,
   "description" : "A ripe pear."
 }
*/
```

## JSONDecoder
An object that decodes instances of a data type from JSON objects.  
从JSON对象解码实例数据的对象。

## Overview
下面的示例显示如何从JSON对象解码简单GroceryProduct类型的实例。 该类型遵循Codable协议，因此可以使用JSONDecoder实例进行解码。

```swift
struct GroceryProduct: Codable {
    var name: String
    var points: Int
    var description: String?
}

let json = """
{
    "name": "Durian",
    "points": 600,
    "description": "A fruit with a distinctive scent."
}
""".data(using: .utf8)!

let decoder = JSONDecoder()
let product = try decoder.decode(GroceryProduct.self, from: json)

print(product.name) // Prints "Durian"
```
