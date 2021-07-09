---
title: swift学习note
date: 2021-07-09 00:24:54
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

### Swift学习note



#### Swift引入

使用 import 语句来引入任何的 Objective-C 框架（或 C 库）到 Swift 程序中。例如 import cocoa 语句导入了使用了 Cocoa 库和API，可以在 Swift 程序中使用它们。

Cocoa 本身由 Objective-C 语言写成，Objective-C 又是 C 语言的严格超集，所以在 Swift 应用中可以很简单的混入 C 语言代码，甚至是 C++ 代码。



#### 分号

Swift不要求在每行语句的结尾使用分号(;)，但在同一行书写多条语句时，必须用分号隔开：

```swift
import Cocoa
var str = "Hello World"; print (str)
```

词法分析或语法分析时应该直接忽略了分号(;)



#### 标识符

如果一定要使用关键字作为标识符，可以在关键字前后添加重音符号（`），例如：

```swift
let `class` = "Runoob"
```

比php中的标识符前加@的处理更高级



#### Swift空格

Swift语言并不是像C/C++，Java那样完全忽视空格，Swift对空格的使用有一定的要求，但是又不像Python对缩进的要求那么严格。

在Swift中，运算符不能直接跟在变量或常量的后面。例如下面的代码会报错：

```swift
let a=1 + 2
```

错误信息是：

```
error: prefix/postfix '=' is reserved
```

意思大概是等号直接跟在前面或后面这种用法是保留的。

下面的代码还是会报错：

```swift
let a = 1+ 2
```

错误信息是：

```
error: consecutive statements on a line must be separated by ';'
```

这是因为Swift认为到1+这个语句就结束了，2就是下一个语句了。

只有这样写才不会报错：

```swift
let a = 1 + 2
let b = 1+2
```

好蠢的设计，为什么不直接忽略空格！？不会用空格来分词吧！那也太不apple了



#### Swift数据类型

Int、UInt、Float、Double、Bool、String、Character（类似cpp）

##### 类型别名

类型别名对当前的类型定义了另一个名字，类型别名通过使用typealias关键字来定义。语法格式如下：

```swift
typealias newname = type
```

类似c中的typedef

##### 类型安全

Swift 是一个类型安全（type safe）的语言。

由于 Swift 是类型安全的，所以它会在编译代码时进行类型检查（type checks），并把不匹配的类型标记为错误。这可以让开发的时候尽早发现并修复错误。

```swift
import Cocoa

var a = 42
a = "hi"
print(a)
```

以上程序，会在Xcode中报错：

```
error: cannot assign value of type 'String' to type 'Int'
varA = "This is hello"
```

意思为不能将 'String' 字符串赋值给 'Int' 变量

##### 常量声明

常量使用关键字let来声明，语法如下：

```swift
let constantName = <initial value>
```

##### 类型标注

当声明常量或者变量的时候可以加上类型标注（type annotation），说明常量或者变量中要存储的值的类型。如果要添加类型标注，需要在常量或者变量名后面加上一个冒号和空格，然后加上类型名称。

```swift
var constantName:<data type> = <optional initial value>
```



#### 区间运算符

Swift 提供了两个区间的运算符

| 运算符         | 描述                                                         | 实例                           |
| -------------- | ------------------------------------------------------------ | ------------------------------ |
| 闭区间运算符   | 闭区间运算符（a...b）定义一个包含从a到b(包括a和b)的所有值的区间，b必须大于等于a。 ‌ 闭区间运算符在迭代一个区间的所有值时是非常有用的，如在for-in循环中 | 1...5 区间值为 1, 2, 3, 4 和 5 |
| 半开区间运算符 | 半开区间（a..<b）定义一个从a到b但不包括b的区间。 之所以称为半开区间，是因为该区间包含第一个值而不包括最后的值 | 1..< 5 区间值为 1, 2, 3, 和 4  |



#### 字符串函数及运算符

Swift 支持以下几种字符串函数及运算符：

| 序号 | 函数/运算符 & 描述                                           |
| :--- | :----------------------------------------------------------- |
| 1    | **isEmpty** 判断字符串是否为空，返回布尔值                   |
| 2    | **hasPrefix(prefix: String)** 检查字符串是否拥有特定前缀     |
| 3    | **hasSuffix(suffix: String)** 检查字符串是否拥有特定后缀。   |
| 4    | **Int(String)** 转换字符串数字为整型。 实例: `let myString: String = "256" let myInt: Int? = Int(myString)` |
| 5    | **String.count** Swift 3 版本使用的是 String.characters.count计算字符串的长度 |
| 6    | **utf8** 可以通过遍历 String 的 utf8 属性来访问它的 UTF-8 编码 |
| 7    | **utf16** 可以通过遍历 String 的 utf8 属性来访问它的 utf16 编码 |
| 8    | **unicodeScalars** 可以通过遍历String值的unicodeScalars属性来访问它的 Unicode 标量编码. |
| 9    | **+** 连接两个字符串，并返回一个新的字符串                   |
| 10   | **+=** 连接操作符两边的字符串并将新字符串赋值给左边的操作符变量 |
| 11   | **==** 判断两个字符串是否相等                                |
| 12   | **<** 比较两个字符串，对两个字符串的字母逐一比较             |
| 13   | **!=** 比较两个字符串是否不相等                              |



#### Swift数组

##### 创建数组

可以使用构造语法来创建一个由特定数据类型构成的空数组：

```swift
var someArray = [SomeType]()
```

以下是创建一个初始化大小数组的语法：

```swift
var someArray = [SomeType](repeating: InitialValue, count: NumbeOfElements)
```

以下实例创建了一个类型为 Int ，数量为 3，初始值为 0 的空数组：

```swift
var someInts = [Int](repeating: 0, count: 3)
```

以下实例创建了含有三个元素的数组：

```swift
var someInts:[Int] = [10, 20, 30]
```



#### Swift字典

##### 创建字典

可以使用以下语法来创建一个特定类型的空字典：

```swift
var someDict =  [KeyType: ValueType]()
```

以下是创建一个空字典，键的类型为 Int，值的类型为 String 的简单语法：

```swift
var someDict = [Int: String]()
```

以下为创建一个字典的实例：

```swift
var someDict:[Int:String] = [1:"One", 2:"Two", 3:"Three"]
```

##### 修改字典

可以使用 updateValue(forKey:) 增加或更新字典的内容。如果 key 不存在，则添加值，如果存在则修改 key 对应的值。updateValue(_:forKey:)方法返回Optional值。实例如下：

```swift
import Cocoa

var someDict:[Int:String] = [1:"One", 2:"Two", 3:"Three"]

var oldVal = someDict.updateValue("One 新的值", forKey: 1)

var someVar = someDict[1]

print( "key = 1 旧的值 \(oldVal)" )
print( "key = 1 的值为 \(someVar)" )
print( "key = 2 的值为 \(someDict[2])" )
print( "key = 3 的值为 \(someDict[3])" )
```

##### 移除Key-Value对

可以使用 removeValueForKey() 方法来移除字典 key-value 对。如果 key 存在该方法返回移除的值，如果不存在返回 nil 。实例如下：

```swift
import Cocoa

var someDict:[Int:String] = [1:"One", 2:"Two", 3:"Three"]

var removedValue = someDict.removeValue(forKey: 2)

print( "key = 1 的值为 \(someDict[1])" )
print( "key = 2 的值为 \(someDict[2])" )
print( "key = 3 的值为 \(someDict[3])" )
```

##### 字典转换为数组

提取字典的键值(key-value)对，并转换为独立的数组。实例如下：

```swift
import Cocoa

var someDict:[Int:String] = [1:"One", 2:"Two", 3:"Three"]

let dictKeys = [Int](someDict.keys)
let dictValues = [String](someDict.values)

print("输出字典的键(key)")

for (key) in dictKeys {
    print("\(key)")
}

print("输出字典的值(value)")

for (value) in dictValues {
    print("\(value)")
}
```



#### Swift函数

##### 元组作为函数返回值

元组与数组类似，不同的是，元组中的元素可以是任意类型，使用的是圆括号。

可以用元组（tuple）类型让多个值作为一个复合值从函数中返回。

下面的这个例子中，定义了一个名为minMax(_:)的函数，作用是在一个Int数组中找出最小值与最大值。

```swift
import Cocoa

func minMax(array: [Int]) -> (min: Int, max: Int) {
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    return (currentMin, currentMax)
}

let bounds = minMax(array: [8, -6, 2, 109, 3, 71])
print("最小值为 \(bounds.min) ，最大值为 \(bounds.max)")
```

##### 外部参数名

可以在局部参数名前指定外部参数名，中间以空格分隔，外部参数名用于在函数调用时传递给函数的参数。

可以定义以下两个函数参数名并调用它：

```swift
import Cocoa

func pow(firstArg a: Int, secondArg b: Int) -> Int {
   var res = a
   for _ in 1..<b {
      res = res * a
   }
   print(res)
   return res
}
pow(firstArg:2, secondArg:3)
```

##### 可变参数

可变参数可以接受零个或多个值。函数调用时，可以用可变参数来指定函数参数，其数量是不确定的。

可变参数通过在变量类型名后面加入（...）的方式来定义

```swift
import Cocoa

func vari<N>(members: N...){
    for i in members {
        print(i)
    }
}
vari(members: 1,2,3)
```

##### 引用参数

一般默认在函数中定义的参数都是常量参数，也就是这个参数你只可以查询使用，不能改变它的值。

如果想要声明一个变量参数，可以在参数定义前加 inout 关键字，这样就可以改变这个参数的值了。

例如：

```swift
func  getName(_ name: inout String)
```

此时这个 name 值可以在函数中改变。

一般默认的参数传递都是传值调用的，而不是传引用。所以传入的参数在函数内改变，并不影响原来的那个参数。传入的只是这个参数的副本。

当传入的参数作为输入输出参数时，需要在参数名前加 & 符，表示这个值可以被函数修改