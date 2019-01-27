---
title: "Key-value coding"
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
## Key-value coding

Key-value coding is a mechanism for indirectly accessing an object’s attributes and relationships using string identifiers. It underpins or is related to several mechanisms and technologies special to Cocoa programming, among them Core Data, application scriptability, the bindings technology, and the language feature of declared properties. (Scriptability and bindings are specific to Cocoa on OS X.) You can also use key-value coding to simplify your program code.  

**Key-value coding是使用字符串标识符间接访问对象的属性和关系的机制。 它支持或与Cocoa编程特有的几种机制和技术相关，其中包括核心数据，应用程序脚本，绑定技术以及声明属性的语言特性。 （脚本性和绑定特定用于OS X上的Cocoa。）您还可以使用Key-value coding来简化程序代码。**

### Object Properties and KVC
Central to key-value coding (or KVC) is the general notion of properties. A property refers to a unit of state that an object encapsulates. A property can be one of two general types: an attribute (for example, name, title, subtotal, or textColor) or a relationship to other objects. Relationships can be either to-one or to-many. The value for a to-many relationship is typically an array or set, depending on whether the relationship is ordered or unordered.  

### 对象属性和KVC
**键值编码（或KVC）的核心是属性的一般概念。 属性是指对象封装的状态单位。 属性可以是两种常规类型之一：属性（例如，名称，标题，小计或字体颜色）或与其他对象的关系。 关系可以to-one也可以是to-many。 To-many关系的值通常是数组或集合，具体取决于关系是有序还是无序。**

KVC locates an object’s property through a key, which is a string identifier. A key usually corresponds to the name of an accessor method or instance variable defined by the object. The key must conform to certain conventions: It must be ASCII encoded, begin with a lowercase letter, and have no whitespace. A key path is a string of dot-separated keys that is used to specify a sequence of object properties to traverse. The property of the first key in the sequence is relative to a specific object (employee1 in the following diagram), and each subsequent key is evaluated relative to the value of the previous property.  

**KVC通过键定位对象的属性，该键是字符串标识符。 Key通常对应于由对象定义的访问器方法或实例变量的名称。Key必须符合某些约定：它必须是`ASCII`编码的，以小写字母开头，并且没有空格。`Key path`是一串点分隔的key，用于指定要穿过的对象属性序列。 序列中第一个key的属性是相对于特定对象（下图中的`employee1`），并且每个后续key相对于前一个属性的值进行计算。**

 ![image1](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/Art/key_value_coding_2x.png) 
  
Making a Class KVC Compliant
The NSKeyValueCoding informal protocol makes KVC possible. Two of its methods—valueForKey: and setValue:forKey:—are particularly important because they fetch and set a property’s value when given its key. NSObject provides a default implementation of these methods, and if a class is compliant with key-value coding, it can rely on this implementation.  

### 使KVC符合Class KVC
**`NSKeyValueCoding`非正式协议使`KVC`成为可能。 它的两个方法-`valueForKey：`和`setValue：forKey：` - 特别重要，因为可以通过为它们指定`key`来获取和设置属性的值。 `NSObject`提供了这些方法的默认实现，并且如果一个类符合`key-value coding`，它可以依赖于这个实现。**

How you make a property KVC compliant depends on whether that property is an attribute, a to-one relationship, or a to-many relationship. For attributes and to-one relationships, a class must implement at least one of the following in the given order of preference (key refers to the property key):

1. The class has a declared property with the name key.
2. It implements accessor methods named key and, if the property is mutable, setKey:. (If the property is a Boolean attribute, the getter accessor method has the form isKey.)
3. It declares an instance variable of the form key or _key.

Implementing KVC compliance for a to-many relationship is a more complicated procedure. Refer to the document that definitively describes key-value coding to learn what this procedure is.  

**如何使属性与KVC兼容，取决于它是一个属性、`to-one`关系，还是`to-many`关系。 对于属性和`to-one`关系，类必须按给定的优先顺序实现以下至少一项（键指的是属性键）：**

**1. 该类具有一个以名称`key`声明的属性。**

**2. 它实现了名为key的访问器方法，如果属性是可变的，则实现setKey：。 （如果属性是布尔属性，则getter访问器方法的格式为isKey。）**

**3.  它以key或_key的形式声明了一个实例变量。**

**为to-many关系实施KVC合规性是一个更复杂的过程。 请参阅明确描述键值编码的文档，以了解此过程。
**
#### Prerequisite Articles
[Object modeling](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/ObjectModeling.html#//apple_ref/doc/uid/TP40008195-CH41-SW1)  
[Accessor method](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/AccessorMethod.html#//apple_ref/doc/uid/TP40008195-CH2-SW1)  

#### Related Articles
[Declared property](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/DeclaredProperty.html#//apple_ref/doc/uid/TP40008195-CH13-SW1)  

#### Definitive Discussion
[Key-Value Coding Programming Guide](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/KeyValueCoding/index.html#//apple_ref/doc/uid/10000107i)