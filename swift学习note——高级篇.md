---
title: swift学习note——高级篇
abbrlink: 48788
date: 2021-07-11 16:45:32
updated:
tags:
categories:
keywords:
description:
top_img:
comments:
cover:
toc:
toc_number:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---

Swift学习note——高级篇

Swift闭包

语法

以下定义了一个接收参数并返回指定类型的闭包语法：

```swift
{(parameters) -> return type in
   statements
}
```

实例

```swift
import Cocoa

let divide = {(val1: Int, val2: Int) -> Int in 
   return val1 / val2 
}
let result = divide(200, 20)
print (result)
```

闭包表达式

闭包表达式是一种利用简洁语法构建内联闭包的方式。 闭包表达式提供了一些语法优化，使得撰写闭包变得简单明了

sorted 方法

Swift 标准库提供了名为 sorted(by:) 的方法，会根据您提供的用于排序的闭包函数将已知类型数组中的值进行排序。

排序完成后，sorted(by:) 方法会返回一个与原数组大小相同，包含同类型元素且元素已正确排序的新数组。原数组不会被 sorted(by:) 方法修改。

sorted(by:)方法需要传入两个参数：

- 已知类型的数组
- 闭包函数，该闭包函数需要传入与数组元素类型相同的两个值，并返回一个布尔类型值来表明当排序结束后传入的第一个参数排在第二个参数前面还是后面。如果第一个参数值出现在第二个参数值前面，排序闭包函数需要返回 true，反之返回 false

实例

```swift
import Cocoa

let names = ["AT", "AE", "D", "S", "BE"]

// 使用普通函数(或内嵌函数)提供排序功能,闭包函数类型需为(String, String) -> Bool。
func backwards(s1: String, s2: String) -> Bool {
    return s1 > s2
}
var reversed = names.sorted(by: backwards)

print(reversed)
```

参数名称缩写

Swift 自动为内联函数提供了参数名称缩写功能，可以直接通过$0,$1,$2来顺序调用闭包的参数

实例

```swift
import Cocoa

let names = ["AT", "AE", "D", "S", "BE"]

var reversed = names.sorted( by: { $0 > $1 } )
print(reversed)
```

如果在闭包表达式中使用参数名称缩写, 可以在闭包参数列表中省略对其定义, 并且对应参数名称缩写的类型会通过函数类型进行推断。in 关键字同样也可以被省略

运算符函数

Swift的String类型定义了关于大于号(>)的字符串实现，其作为一个函数接受两个String类型的参数并返回Bool类型的值。而这正好与sort(_:)方法的第二个参数需要的函数类型相符合。因此，您可以简单地传递一个大于号，Swift可以自动推断出您想使用大于号的字符串函数实现：

```swift
import Cocoa

let names = ["AT", "AE", "D", "S", "BE"]

var reversed = names.sorted(by: >)
print(reversed)
```

尾随闭包

尾随闭包是一个书写在函数括号之后的闭包表达式，函数支持将其作为最后一个参数调用

实例

```swift
import Cocoa

let names = ["AT", "AE", "D", "S", "BE"]

//尾随闭包
var reversed = names.sorted() { $0 > $1 }
print(reversed)
```

如果函数只需要闭包表达式一个参数，当使用尾随闭包时，甚至可以把()省略掉

```swift
reversed = names.sorted { $0 > $1 }
```

捕获值

闭包可以在其定义的上下文中捕获常量或变量。

即使定义这些常量和变量的原域已经不存在，闭包仍然可以在闭包函数体内引用和修改这些值。

Swift最简单的闭包形式是嵌套函数，也就是定义在其他函数的函数体内的函数。

嵌套函数可以捕获其外部函数所有的参数以及定义的常量和变量。

实例：

```swift
func makeIncrementor(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func incrementor() -> Int {
        runningTotal += amount
        return runningTotal
    }
    return incrementor
}
```

一个函数makeIncrementor ，它有一个Int型的参数amout, 并且它有一个外部参数名字forIncremet，意味着你调用的时候，必须使用这个外部名字。返回值是一个()-> Int的函数。

函数体内，声明了变量 runningTotal 和一个函数 incrementor。

incrementor函数并没有获取任何参数，但是在函数体内访问了runningTotal和amount变量。这是因为其通过捕获在包含它的函数体内已经存在的runningTotal和amount变量而实现。

由于没有修改amount变量，incrementor实际上捕获并存储了该变量的一个副本，而该副本随着incrementor一同被存储。

所以我们调用这个函数时会累加：

```swift
import Cocoa

func makeIncrementor(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func incrementor() -> Int {
        runningTotal += amount
        return runningTotal
    }
    return incrementor
}

let incrementByTen = makeIncrementor(forIncrement: 10)

// 返回的值为10
print(incrementByTen())

// 返回的值为20
print(incrementByTen())

// 返回的值为30
print(incrementByTen())
```

闭包是引用类型

上面的例子中，incrementByTen是常量，但是这些常量指向的闭包仍然可以增加其捕获的变量值。

这是因为函数和闭包都是引用类型。

无论您将函数/闭包赋值给一个常量还是变量，您实际上都是将常量/变量的值设置为对应函数/闭包的引用。 上面的例子中，incrementByTen指向闭包的引用是一个常量，而并非闭包内容本身。

这也意味着如果您将闭包赋值给了两个不同的常量/变量，两个值都会指向同一个闭包：

```swift
import Cocoa

func makeIncrementor(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func incrementor() -> Int {
        runningTotal += amount
        return runningTotal
    }
    return incrementor
}

let incrementByTen = makeIncrementor(forIncrement: 10)

// 返回的值为10
incrementByTen()

// 返回的值为20
incrementByTen()

// 返回的值为30
incrementByTen()

// 返回的值为40
incrementByTen()

let alsoIncrementByTen = incrementByTen

// 返回的值也为50
print(alsoIncrementByTen())
```

