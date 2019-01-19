---
title: "构造器"
layout: post
date: 2019-01-20 00:07
image: /assets/images/swift_logo.png
headerImage: true
tag:
- swift
star: false
category: blog
author: james
description: learning swift
---
## 为存储属性设置初始化值
在创建类和结构体的实例时***必须***为所有的存储属性设置一个合适的初始值。存储属性不能遗留在不确定的状态中。

## 自定义初始化
### 在初始化中分配常量属性
对于类实例来说，常量属性在初始化中只能通过引用的类来修改。它不能被子类修改。

## 默认构造器
Swift 为所有***没有提供自定义构造器***的结构体或类提供了一个默认的构造器来给所有的属性提供了默认值。

## 类的继承和初始化
类的所有存储属性——包括从它的父类继承的所有属性——都必须在初始化期间分配初始值。  

每个类至少得有一个指定初构造器。在某些情况下，这些需求通过从父类继承一个或多个指定构造器来满足。

### 类类型的构造器委托

* 指定构造器必须总是向上委托。
*  便捷构造器必须总是横向委托。

### 两段式初始化
In the first phase, each stored property is assigned an initial value by the class that introduced it.  
第一个阶段，每个存储属性都会被**引入它的类**分配一个初始值。  
一旦每个存储属性的初始状态被确定，第二个阶段就开始了，每个类都有机会在新的实例准备使用之前来定制它的存储属性。

#### 安全检查 1
指定构造器必须保证在向上委托给父类构造器之前，其**自己的所有属性都要初始化完成**。 
 
一个对象的**内存**只有在其所有储存型***属性***确定之后才能完全初始化。

#### 安全检查 2
指定构造器必须先向上委托父类构造器，然后才能为***继承来的属性***设置新值。否则，其赋的值会被父类的构造器覆盖。

#### 安全检查 3
便捷构造器必须先委托同类中的其它构造器，然后再为任意属性赋新值（包括同类里定义的属性）。否则，其所赋的值会被当前类的指定构造器覆盖。

#### 安全检查 4
构造器在第一阶段初始化完成之前，不能调用任何实例方法、不能读取任何实例属性的值，也不能引用 self 作为值。直到第一阶段结束类实例才完全合法，至此，属性才能被读取，方法也才能被调用。

#### 阶段 1

* 指定或便捷构造器在类中被调用；
* 为这个类的新实例分配内存，内存还没有被初始化；
* 类的指定构造器确保所有自己的存储属性都有一个值，而后这些存储属性的内存被初始化了；
* 指定构造器通知父类的构造器，为其存储属性执行相同的任务；
* 这个调用父类构造器的过程将沿着构造器链一直向上进行，直到到达构造器链的最顶部；
* 一旦达了构造器链的最顶部，在链顶部的**基类**确保**自己和所有子类**的存储属性都有一个值，此实例的内存被认为**完全**初始化了，此时第一阶段完成。

#### 阶段 2

* 从顶部构造器往下，链中的每一个指定构造器都有机会进一步定制实例。构造器现在能够访问 `self` 并且可以修改它的属性，调用它的实例方法等等；
* 最终，链中任何便捷构造器都有机会定制实例以及使用 `self` 。

第二阶段，父类的指定构造器有机会来定制更多实例(尽管没有这种必要)。

一旦父类的指定构造器完成了调用，子类的指定初始化器就可以执行额外的定制(同样，尽管没有这种必要)。

最后，一旦子类的指定构造器完成，最初调用的便捷初始化器将会执行额外的定制操作。

### 构造器的继承和重写
1. 当重写父类指定初始化器时，你必须写 override 修饰符，override 修饰符会让 Swift 来检查父类是否有一个匹配的指定初始化器来重写，并且验证你重写的初始化器已经按照意图指定了形式参数。
2. 如果你写了一个匹配父类便捷初始化器的子类初始化器，父类的便捷初始化器将永远不会通过你的子类直接调用。因此，你的子类不能(严格来讲)提供父类初始化器的重写。当提供一个匹配的父类便捷初始化器的实现时，你不用写 override 修饰符。

默认初始化器(如果可用的话)总是类的指定初始化器。

### 初始化器的自动继承

子类默认不会继承父类初始化器。然而，在特定的情况下父类初始化器是可以被自动继承的。实际上，这意味着在许多场景中你不必重写父类初始化器，只要可以安全操作，你就可以毫不费力地继承父类的初始化器。

假设你为你子类引入的任何新的属性都提供了默认值，请遵守以下2个规则：
#### 规则 1
如果你的子类没有定义任何指定初始化器，它会自动继承父类所有的指定初始化器。

#### 规则 2 
如果你的子类提供了所有父类指定初始化器的实现，那么它自动继承所有的父类便捷初始化器。

A subclass can implement a superclass designated initializer as a subclass convenience initializer as part of satisfying rule 2.   
为了满足规则2，子类可以把父类的指定构造器当作自己的便捷构造器来实现。

### 指定和便捷初始化器的实战

```swift
class Food {
    var name: String
    init(name: String) {
        self.name = name
    }
    convenience init() {
        self.init(name: "[Unnamed]")
    }
}


class RecipeIngredient: Food {
    var quantity: Int
    init(name: String, quantity: Int) {
        self.quantity = quantity
        super.init(name: name)
    }
    
    // 如果没有这个便捷构造器，也就没有提供父类的指定构造器的实现，
    // 所以就不能继承父类的便捷构造器 init（）
    // 第26句也就会在编译时报错
    override convenience init(name: String) {
        self.init(name: name, quantity: 1)
    }
}

let mysteryIngredient = RecipeIngredient()
```

如果为自己引入的所有属性提供了一个默认值并且自己没有定义任何初始化器， 子类就会自动继承父类**所有的指定和便捷初始化器**。

## 可失败初始化器
★ 不能定义可失败和非可失败的初始化器为相同的形式参数类型和名称。  

★ 可以通过检查实例是否为`nil`，来查看构造是否成功。

```swift
let anonymousCreature = Animal(species: "")
// anonymousCreature is of type Animal?, not Animal
 
if anonymousCreature == nil {
    print("The anonymous creature could not be initialized")
}
// prints "The anonymous creature could not be initialized"
```

### 枚举的可失败初始化器
You can use a failable initializer to select an appropriate enumeration case based on one or more parameters.   
可以用一个可失败的构造器为枚举选择一个合适的成员值（case），这个成员值的选定基于该构造器的一个或多个参数。如果提供的参数不能匹配合适的成品值，则构造失败。

```swift
enum TemperatureUnit {
    case kelvin, celsius, fahrenheit
    init?(symbol: Character) {
        switch symbol {
        case "K":
            self = .kelvin
        case "C":
            self = .celsius
        case "F":
            self = .fahrenheit
        default:
            return nil
        }
    }
}
```

### 带有原始值枚举的可失败初始化器
带有原始值的枚举会自动获得一个可失败初始化器 `init?(rawValue:)`，该可失败初始化器接收一个名为 `rawValue` 的合适的原始值类型形式参数如果找到了匹配的枚举情况就选择其一，或者没有找到匹配的值就触发初始化失败。

```swift
enum TemperatureUnit: Character {
    case Kelvin = "K", Celsius = "C", Fahrenheit = "F"
}
```

### 初始化失败的传递
可失败初始化器可以横向委托到自己的另一个可失败初始化器。类似地，子类的可失败初始化器可以向上委托到父类的可失败初始化器。

无论哪种情况，如果你委托到另一个初始化器导致了初始化失败，那么整个初始化过程也会立即失败，并且之后任何初始化代码都不会执行。

### 重写可失败初始化器
你可以用子类的非可失败初始化器来重写父类可失败初始化器。  
★ 你可以用一个非可失败初始化器重写一个可失败初始化器，但反过来是不行的。

## 必要初始化器
You do not have to provide an explicit implementation of a required initializer if you can satisfy the requirement with an inherited initializer.  
如果子类继承的初始化器能够满足需求，则你无需显式地在子类中提供必要初始化器的实现。

## 通过闭包和函数来设置属性的默认值
 
如果存储属性的默认值需要自定义或设置，可以用一个闭包或者全局函数去自定义这个属性。无论何时，当此类型（包含该属性）的一个新的实例被初始化，闭包或者全局函数就被调用，它的返回值就是属性的默认值。

```swift
class SomeClass {
    let someProperty: SomeType = {
        // create a default value for someProperty inside this closure
        // someValue must be of the same type as SomeType
        return someValue
    }()  // 注意圆括号
}
```
注意闭包花括号的结尾跟一个没有参数的圆括号。这是告诉 Swift 立即执行闭包。如果你忽略了这对圆括号，你就会把闭包作为值赋给了属性，并且不会返回闭包的值。  

***★ 如果你使用了闭包来初始化属性，请记住闭包执行的时候，实例的其他部分还没有被初始化。这就意味着你不能在闭包里读取任何其他的属性值，即使这些属性有默认值。你也不能使用隐式 self 属性，或者调用实例的方法。***