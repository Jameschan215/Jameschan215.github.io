---
title: "Key-Value Coding Programming Guide(part)"
layout: post
date: 2019-01-27 17:21
image: /assets/images/swift_logo.png
headerImage: true
tag:
- translate
star: false
category: blog
author: james
description: swift standard library
---
## 兼容KVC的对象
通常地，继承（直接或间接）自NSObject的对象自动采用key-value coding，它们都遵循NSKeyValueCoding协议，并为其基本方法提供默认实现。 这样的对象通过紧凑的消息传递接口使其他对象能够执行以下操作： 
 
* **访问对象属性。** 该协议指定方法，例如泛型*getter* `valueForKey：`和泛型*setter* `setValue：forKey：`，用于按名称或键访问对象属性，参数化为字符串。 这些默认的实现和一些相关的方法使用键来定位基础数据并与其交互，如[访问对象属性](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/KeyValueCoding/BasicPrinciples.html#//apple_ref/doc/uid/20002170-BAJEAIEE)中所述。
*  **操作集合属性。** 访问方法的默认实现使用对象的集合属性（例如NSArray对象），就像任何其他属性一样。 此外，如果对象为属性定义了一个集合访问器方法，则它允许对集合内容进行键值访问。 这通常比直接访问更有效，并允许您通过标准化界面使用自定义集合对象，如[访问集合属性](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/KeyValueCoding/AccessingCollectionProperties.html#//apple_ref/doc/uid/10000107i-CH4-SW1)中所述。
*  **在集合对象上调用集合运算符。** 在符合键值编码的对象中访问集合属性时，可以将*集合运算符*插入到键字符串中，如[使用集合运算符中](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/KeyValueCoding/CollectionOperators.html#//apple_ref/doc/uid/20002176-BAJEAIEE)所述。 集合运算符指示默认的`NSKeyValueCoding`getter实现对集合执行操作，然后返回集合的新的过滤版本或表示集合某些特征的单个值。
*  **访问非对象属性。** 协议的默认实现检测非对象属性，包括标量和结构，并自动将它们包装和解包为协议接口上使用的对象，如[表示非对象值](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/KeyValueCoding/DataTypes.html#//apple_ref/doc/uid/20002171-BAJEAIEE)中所述。 此外，该协议声明了一种方法，当非对象属性被设置为`nil`时，该方法允许兼容对象通过键值编码接口为该情况提供合适的动作。
*  **利用`key path`访问属性。** 如果您具有符合键值编码的对象的层次结构，则可以使用基于`key path`的方法,使用单个调用在层次结构中深入查看、获取或设置值。

## 为对象采用Key-value Coding
为了使您自己的对象符合键值编码，您需要确保它们遵循了NSKeyValueCoding非正式协议并实现相应的方法，例如valueForKey：作为通用getter和setValue：forKey：作为通用setter。 幸运的是，如上所述，NSObject采用此协议并为这些和其他基本方法提供默认实现。 因此，如果从NSObject（或其任何子类）派生对象，则上述大部分工作已经自动为您完成。  

为了使默认方法完成其工作，您需要确保对象的访问器方法和实例变量遵循某些明确定义的模式。 这允许默认实现查找对象的属性以响应KVC消息。 然后，通过提供方法来认可和处理某些特殊情况，您可以扩展和自定义KVC。

## Swift中使用KVC
Swift objects that inherit from NSObject or one of its subclasses are key-value coding compliant for their properties by default. Whereas in Objective-C, a property’s accessors and instance variables must follow certain patterns, a standard property declaration in Swift automatically guarantees this. On the other hand, many of the protocol’s features are either not relevant or are better handled using native Swift constructs or techniques that do not exist in Objective-C. For example, because all Swift properties are objects, you never exercise the default implementation’s special handling of non-object properties.