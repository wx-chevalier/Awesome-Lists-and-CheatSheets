# Swift CheatSheet | Swift 语法与实践清单

## 注释与换行

### 注释

请将你的代码中的非执行文本注释成提示或者笔记以方便你将来阅读。Swift 的编译器将会在编译代码时自动忽略掉注释部分。

Swift 中的注释与 C 语言的注释非常相似。单行注释以双正斜杠作(//)为起始标记:

```swift
// 这是一个注释
```

你也可以进行多行注释，其起始标记为单个正斜杠后跟随一个星号(/_)，终止标记为一个星号后跟随单个正斜杠(_/):

```
/* 这是一个, 多行注释 */
```

与 C 语言多行注释不同，Swift 的多行注释可以嵌套在其它的多行注释之中。你可以先生成一个多行注释块，然后在这个注释块之中再嵌套成第二个多行注释。终止注释时先插入第二个注释块的终止标记，然后再插入第一个注释块的终止标记：

```
/* 这是第一个多行注释的开头 /* 这是第二个被嵌套的多行注释 */ 这是第一个多行注释的结尾 */
```

通过运用嵌套多行注释，你可以快速方便的注释掉一大段代码，即使这段代码之中已经含有了多行注释块。

### Swift 类引用 Objective-C 文件

因为 Swift 没有内嵌的头文件机制，因此 Swift 调用 Objective-C 需要一个名为“<工程名>-Bridging-Header.h”的桥接头文件。桥接头文件的作用是为 Swift 调用 Objective-C 对象搭建一个桥，它的命名必须是“<工程名>- Bridging-Header.h”，我们需要在桥接头文件中引入 Objective-C 头文件，所有的 Swift 类会自动引用这个头文件。

![桥接文件](http://www.ituring.com.cn/figures/2014/Swift/19.d18z.001.png)

![桥接文件设置](http://img.blog.csdn.net/20140627164025671?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaHVhbmdjaGVudGFv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

- OJC 类如下：

```objective-c
//
//  ObjcFunc.h
//

# import <Foundation/Foundation.h>

@interface ObjcFunc : NSObject

-(NSString*)sayHello:(NSString*)greeting withName: (NSString*)name;

@end

//
//  ObjcFunc.m
//

# import "ObjcFunc.h"

# import "CombinedProgram-Swift.h"

@implementation ObjcFunc

- (NSString*)sayHello:(NSString*)greeting withName: (NSString*)name{

    NSString *string = [NSString stringWithFormat:@"Hi,%@ %@.",name,greeting];

    return string;

  }

@end
```

- Swift 类中调用

```
import Foundation
@objc class SwiftFunc: NSObject {
  func sayHello() -> Void {
  var obj : ObjcFunc = ObjcFunc()
  println(obj.sayHello("Hello", withName: "Swift"));
  return
  }
}
```

### Objective-C 类引用 Swift 文件

(1)在 Building Settings -> Packaging -> Defining 中选定 Module Name；

(2)在 OJC 的头文件中引入：`#import "{ModuleName}-swift.h"`

```swift
SwiftFunc* obj = [[SwiftFunc alloc] init];
[obj sayHello];
```

有时候会发现 Xcode 无法自动生成\*-Swift.h 文件，可以参考[StackOverflow][9]上的这篇文章。该文章总结下来，我们需要进行以下两大步检测：

(1)检测你的 Xcode 的配置

```
Product Module Name : myproject

Defines Module : YES

Embedded Content Contains Swift : YES

Install Objective-C Compatibility Header : YES

sObjective-C Bridging Header : $(SRCROOT)/Sources/SwiftBridging.h
```

(2)检查你的 Swift 类是否正规

要保证你的 Swfit 类中已经使用@objc 关键字声明了一个继承自 NSObject 的类。Xcode 不会为存在任何编译错误的类进行编译操作。

(3)忽略 Xcode 的报错，先编译一下

# 流程控制

## 分支选择

### if

```swift
if 1+1 == 2 {
         println("The math checks out")
}
```

### if-let

可以用 if-let 语句检查一个可选变量是否包 含值。如果包含,则将这个值指定给一个常量变量,然后运行某段代码。这样可以减少很多行代码,同时又能够保证安全性

```swift
var conditionalString : String? = "a string"
     if let theString = conditionalString? {
         println("The string is '\(theString)'")
     } else {
         println("The string is nil")
}
// 输出 "The string is 'a string'"
```

## 循环

### for

### for-in

```swift
let loopingArray = [1,2,3,4,5]
var loopSum = 0
for number in loopingArray {
     loopSum += number
}
loopSum // = 15


var firstCounter = 0
     for index in 1 ..< 10 {
         firstCounter++
     }
// 循环9次

var secondCounter = 0
for index in 1 ... 10 { // 注意是三个句点,不是两个
         secondCounter++
     }
// 循环10次

var sum = 0
for var i = 0; i < 3; i++ {
    sum += 1
}
sum // = 3
```

### while

```swift
var countDown = 5
while countDown > 0 {
     countDown--
}
countDown // = 0

var countUP = 0
do {
         countUp++
} while countUp < 5
countUp // = 5
```

# 函数

## 函数定义

当你定义一个函数时，你可以选择性地定义一个或多个名称，类型值作为函数的输入(称为形参)，或者定义一个函数结束后返回值的类型(称之为返回型)。每一个函数都有一个函数名，用来描述了函数执行的任务。要使用一个函数时，可使用它的名称进行“调用”，并通过它的输入值(称为实参--argument)来匹配函数的参数类型。**一个函数的实参(arguments)必须始终和函数形参(parameter)顺序一致**。

```swift
func sayHello(personName: String) -> String {
  let greeting = "Hello, " + personName + "!"
  return greeting
}

println(sayHello("Anna"))
// prints "Hello, Anna!"
println(sayHello("Brian"))
// prints "Hello, Brian!"
```

### 函数返回值

由于 Swift 中存在元组类型(tuples)，所以 Swift 允许有多个返回值或者直接无返回值。

#### 无返回值函数

函数不需要定义一个返回类型。这里有一个版本的 sayHello 函数，称为 waveGoodbye，它会打印自己的 String 值而不是返回它：

```swift
func sayGoodbye(personName: String) {
	println("Goodbye, \(personName)!")
}
sayGoodbye("Dave") // prints "Goodbye, Dave!"
```

严格地说，sayGoodbye 函数确实还返回一个值，即使没有定义返回值。没有定义返回类型的函数返回了一个 Void 类型的特殊值。这仅是一个空元组，这里边没有元素，可以被写成()。

#### 单返回值函数

两个参数一个返回值，都为 Int

```swift
func thirdFunction(firstValue: Int, secondValue: Int) -> Int {
         return firstValue + secondValue
     }
thirdFunction(1, 2)
```

#### 多返回值函数

可以使用一个元组类型作为函数的返回类型，来返回一个由多个值组成的复合返回值。下面的例子定义了一个名为 count 函数，用来计算字符串中基于标准美式英语的元音、辅音以及字符的数量：

```swift
func count(string: String) -> (vowels: Int, consonants: Int, others: Int) {
        var vowels = 0, consonants = 0, others = 0
        for character in string {
            switch String(character).lowercaseString {
            case "a", "e", "i", "o", "u":
                ++vowels
            case "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
            "n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z":
            ++consonants
            default:
            ++others
            }
        }
        return (vowels, consonants, others)
    }
```

上文中关于元组部分讲解时也提及，可以直接利用下标或者属性名来访问元组中值，因此，多返回值也可以这么使用：

```swift
func fourthFunction(firstValue: Int, secondValue: Int)
         -> (doubled: Int, quadrupled: Int) {
         return (firstValue * 2, secondValue * 4)
     }
fourthFunction(2, 4)

// 用数字访问:
fourthFunction(2, 4).1 // = 16

// 其他相同,只是使用了名字:
fourthFunction(2, 4).quadrupled // = 16
```

### 函数变量

```
var numbersFunc: (Int, Int) -> Int;
// numbersFunc现在可以存储任何接受两个Int并返回一个Int的函数

numbersFunc = addNumbers
numbersFunc(2, 3) // = 5
```

## 参数调用

### 本地形参与外部形参

> 注意，全局函数中不可以使用外部形参

所有上面的函数都为其形参定义了形参名：

```swift
    func someFunction(parameterName: Int) {
        // function body goes here, and can use parameterName
        // to refer to the argument value for that parameter
    }
```

然而，这些参数名的仅能在函数本身的主体内使用，不能在调用函数时使用。这种形参类型名称被称之为本地形参名(local parameter name)，因为它们只能在函数的主体中使用。有时当你调用一个函数将每个形参进行命名是非常有用的，以表明你把每个实参传递给函数的目的。如果你希望使用你函数的人在调用函数时提供形参名称，那除了本地形参名外，你还要为每个形参定义一个外部形参名称。你写一个外部形参名称在它所支持的本地形参名称之前,之间用一个空格来分隔:

```swift
func someFunction(externalParameterName localParameterName: Int) {
        // function body goes here, and can use localParameterName
        // to refer to the argument value for that parameter
    }

    func join(string s1: String, toString s2: String, withJoiner joiner: String)
        -> String {
        return s1 + joiner + s2
    }
    join(string: "hello", toString: "world", withJoiner: ", ")
    // returns "hello, world"
```

#### 外部参数名称速记

如果你想为一个函数提供一个外部形参名，然而本地形参名已经使用了一个合适的名称了，那你就不需要两次书写该形参的名称。相反，你可以写一次名字，并用一个 hash 符号(＃)作为名称的前缀。这就告诉 Swift 使用名称相同的本地行参名称和外部形参名称。这个例子定义了一个名为 containsCharacter 的函数,通过在本地形参名前添加 hash 符号(#)来定义外部形参名称。

```swift
func containsCharacter(#string: String, #characterToFind: Character) -> Bool {
    for character in string {
        if character == characterToFind {
            return true
        }
    }
    return false
}
```

该函数对形参名的选择使得其函数主题更加清晰易读，并且在调用该函数时也不会有歧义：

```swift
let containsAVee = containsCharacter(string: "aardvark", characterToFind: "v")
// containsAVee equals true, because "aardvark" contains a "v"
```

### 默认形参值

```
你可以为任何形参定义默认值以作为函数定义的一部分。如果已经定义了默认值，那么调用函数时就可以省略该行参。
```

> 注意：请在函数形参列表的末尾放置带默认值的形参。这将确保所有函数调用都使用顺序相同的无默认值实参，并让在每种情况下清晰地调用相同的函数。

```
这里有一个早期的join函数，并为参数joiner设置了默认值：
```

```swift
func join(string s1: String, toString s2: String,
    withJoiner joiner: String = " ") -> String {
        return s1 + joiner + s2
}
```

```
如果在join函数调用时为joiner提供了字符串值，那么该字符串值可以用来连接两个字符串，就跟以前一样：
```

```swift
    join(string: "hello", toString: "world", withJoiner: "-")
    // returns "hello-world"
```

```
但是，如果函数调用时没有为joiner提供值，就会使用单个空格(" ")的默认值：
```

```swift
    join(string: "hello", toString: "world")
    // returns "hello world"
```

### 不定形参

```
一个可变形参可接受零个或多个指定类型的值。当函数被调用时，你可以使用可变形参来指定--形参可以用来传递任意数量的输入值。可通过在形参的类型名后边插入三个点符号(...)来编写可变形参。传递至可变形参的值在函数主体内是以适当类型的数组存在的。例如,一个可变参数的名称为numbers和类型为Double...在函数体内就作为名为numbers类型为Double[]的常量数组。
```

> 注意：函数最多可以有一个可变形参，而且它必须出现在参数列表的最后，以避免使用多个形参调用函数引发歧义。如果你的函数有一个或多个带有默认值的形参，并且还有可变形参，请将可变形参放在所有默认形参之后，也就是的列表的最末尾。

```swift
    func arithmeticMean(numbers: Double...) -> Double {
        var total: Double = 0
        for number in numbers {
            total += number
        }
        return total / Double(numbers.count)
    }
    arithmeticMean(1, 2, 3, 4, 5)
    // returns 3.0, which is the arithmetic mean of these five numbers
    arithmeticMean(3, 8, 19)
    // returns 10.0, which is the arithmetic mean of these three numbers
```

#### 常量形参和变量形参

```
**函数的形参默认是常量**。试图在函数体内改变函数形参的值会引发一个编译时错误。这意味着你不能错误地改变形参的值。但是有时候，函数有一个形参值的变量副本是非常有用的。您可以指定一个或多个形参作为变量形参，从而避免在函数内部为自己定义一个新的变量。变量参数是变量而非常量,并给函数一个可修改的形参值副本。
```

```swift
    func alignRight(var string: String, count: Int, pad: Character) -> String {
        let amountToPad = count - countElements(string)
        for _ in 1...amountToPad {
            string = pad + string
        }
        return string
    }
    let originalString = "hello"
    let paddedString = alignRight(originalString, 10, "-")
    // paddedString is equal to "-----hello"
    // originalString is still equal to "hello"
```

#### In-Out 形参

如上描述，变量形参只能在函数本身内改变。如果你想让函数改变形参值，并想要在函数调用结束后保持形参值的改变，那你可以把形参定义为 in-out 形参。通过在形参定义的开始添加 inout 关键字来编写 in-out 形参。In-Out 形参有一个传递至函数的值，由函数修改，并从函数返回来替换原来的值。你只能传递一个变量作为 in-out 形参对应的实参。你不能传递一个常量或者字面量作为实参，因为常量和字面量不能被修改。当你把变量作为实参传递给 in out 形参时，需要在直接在变量前添加 & 符号，以表明它可以被函数修改。

> 提示：in-out 参数不能有默认值，可变参数的参数也不能被标记为 inout。如果您标记参数为 inout，它不能同时被标记为 var 或 let。

```swift
    func swapTwoInts(inout a: Int, inout b: Int) {
        let temporaryA = a
        a = b
        b = temporaryA
    }
```

```
swapTwoInts函数只是简单地交换a、b的值。该函数通过存储一个名为temporaryA临时常量的值，指定b的值到a，然后分配temporaryA到b执行该交换。你可以通过两个Int类型的变量调用swapTwoInts函数，从而交换它们的值。需要注意的是当它们被传递给swapTwoInts函数时，someInt和anotherInt名称前要加上前缀符号&：
```

```swift
    var someInt = 3
    var anotherInt = 107
    swapTwoInts(&someInt, &anotherInt)
    println("someInt is now \(someInt), and anotherInt is now \(anotherInt)")
    // prints "someInt is now 107, and anotherInt is now 3"
```

## 函数类型

## 闭包

闭包可以**捕获**和存储其所在上下文中任意常量和变量的**引用**。这就是所谓的闭合并包裹着这些常量和变量，俗称闭包。Swift 会为您管理在**捕获**过程中涉及到的内存操作。在 函数 章节中介绍的全局和嵌套函数实际上也是特殊的闭包，闭包采取如下三种形式之一：

1.全局函数是一个有名字但不会捕获任何值的闭包

2.嵌套函数是一个有名字并可以捕获其封闭函数域内值的闭包

3.闭包表达式是一个利用轻量级语法所写的可以捕获其上下文中变量或常量值的没有名字的闭包

### 闭包表达式

闭包表达式的语法有如下形式：

```
{ (parameters) -> returnType in
    statements
}
```

闭包表达式语法可以使用常量、变量和 inout 类型作为参数，但不提供默认值。也可以在参数列表的最后使用可变参数。元组也可以作为参数和返回值。下面的例子展示了之前 backwards 函数对应的闭包表达式版本的代码：

```swift
    reversed = sort(names, { (s1: String, s2: String) -> Bool in
        return s1 > s2
    })
```

需要注意的是内联闭包参数和返回值类型声明与 backwards 函数类型声明相同。在这两种方式中，都写成了 (s1: String, s2: String) -> Bool 类型。然而在内联闭包表达式中，函数和返回值类型都写在大括号内，而不是大括号外。闭包的函数体部分由关键字 in 引入。该关键字表示闭包的参数和返回值类型定义已经完成，闭包函数体即将开始。

#### 根据上下文推断类型

因为排序闭包是作为函数的参数进行传入的，Swift 可以推断其参数和返回值的类型。sort 期望第二个参数是类型为 (String, String) -> Bool 的函数，因此实际上 String, String 和 Bool 类型并不需要作为闭包表达式定义中的一部分。因为所有的类型都可以被正确推断，返回箭头 (->) 和 围绕在参数周围的括号也可以被省略：

```swift
	reversed = sort(names, { s1, s2 in return s1 > s2 } )
```

#### 单行表达式闭包可以省略 return

单行表达式闭包可以通过隐藏 return 关键字来隐式返回单行表达式的结果，如上版本的例子可以改写为：

```swift
    reversed = sort(names, { s1, s2 in s1 > s2 } )
```

#### 参数名简写

Swift 自动为内联函数提供了参数名称简写功能，您可以直接通过 $0,$1,\$2 等名字来引用的闭包的参数的值。如果您在闭包表达式中使用参数名称简写，您可以在闭包参数列表中省略对其的定义，并且对应参数名称简写的类型会通过函数类型进行推断。in 关键字也同样可以被省略，因为此时闭包表达式完全由闭包函数体构成：

```swift
	reversed = sort(names, { $0 > $1 } )
```

#### Trailing 闭包

如果您需要将一个很长的闭包表达式作为最后一个参数传递给函数，可以使用 trailing 闭包来增强函数的可读性。Trailing 闭包是一个书写在函数括号之外(之后)的闭包表达式，函数支持将其作为最后一个参数调用。

```swift
    func someFunctionThatTakesAClosure(closure: () -> ()) {
        // 函数体部分
    }

    // 以下是不使用 trailing 闭包进行函数调用

    someFunctionThatTakesAClosure({
        // 闭包主体部分
    })

    // 以下是使用 trailing 闭包进行函数调用

    someFunctionThatTakesAClosure() {
        // 闭包主体部分
    }
```

在上例中作为 sort 函数参数的字符串排序闭包可以改写为：

```
reversed = sort(names) { $0 > $1 }
```

### 捕获(Capture)

闭包可以在其定义的上下文中捕获常量或变量。即使定义这些常量和变量的原作用域已经不存在，闭包仍然可以在闭包函数体内引用和修改这些值。Swift 最简单的闭包形式是嵌套函数，也就是定义在其他函数体内的函数。嵌套函数可以捕获其外部函数所有的参数以及定义的常量和变量。下例为一个叫做 makeIncrementor 的函数，其包含了一个叫做 incrementor 嵌套函数。嵌套函数 incrementor 从上下文中捕获了两个值，runningTotal 和 amount。之后 makeIncrementor 将 incrementor 作为闭包返回。每次调用 incrementor 时，其会以 amount 作为增量增加 runningTotal 的值。

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

```
incrementor 函数并没有获取任何参数，但是在函数体内访问了 runningTotal 和 amount 变量。这是因为其通过捕获在包含它的函数体内已经存在的runningTotal 和 amount 变量而实现。

由于没有修改 amount 变量，incrementor 实际上捕获并存储了该变量的一个副本，而该副本随着 incrementor 一同被存储。然而，因为每次调用该函数的时候都会修改 runningTotal 的值，incrementor 捕获了当前 runningTotal 变量的引用，而不是仅仅复制该变量的初始值。捕获一个引用保证了当 makeIncrementor 结束时候并不会消失，也保证了当下一次执行 incrementor 函数时，runningTotal 可以继续增加。
```

下面为一个使用 makeIncrementor 的例子：

```
let incrementByTen = makeIncrementor(forIncrement: 10)
```

```
该例子定义了一个叫做 incrementByTen 的常量，该常量指向一个每次调用会加10的 incrementor 函数。调用这个函数多次可以得到以下结果：
```

```swift
incrementByTen() // 返回的值为10
incrementByTen() // 返回的值为20
incrementByTen() // 返回的值为30
```

如果您创建了另一个 incrementor，其会有一个属于自己的独立的 runningTotal 变量的引用。下面的例子中，incrementBySevne 捕获了一个新的 runningTotal 变量，该变量和 incrementByTen 中捕获的变量没有任何联系：

```swift
let incrementBySeven = makeIncrementor(forIncrement: 7)
incrementBySeven() // 返回的值为7
incrementByTen() // 返回的值为40
```

# 类与对象

## 定义与实例化

类的基本的定义方式如下所示：

```swift
class Vehicle {
    var color: String?
    var maxSpeed = 80
    func description() -> String {
        return "A \(self.color) vehicle"
    }
    func travel() {
        print("Traveling at \(maxSpeed) kph")
    }
}
```

### 实例化

最简单的实例化方法：

```swift
var redVehicle = Vehicle()
redVehicle.color = "Red"
redVehicle.maxSpeed = 90
redVehicle.travel() // 输出"Traveling at 90 kph" redVehicle.description() // = "A Red vehicle"
```

也可以重载类的构造函数，使之能够有不同的参数：

```swift
class InitAndDeinitExample {
    // 指定的初始化器(也就是主初始化器)
    init() {
        print("I've been created!")
    }
    // 便捷初始化器,是调用上述指定初始化器所必需的
    convenience init (text: String) {
        self.init() // 这是必需的
        print("I was called with the convenience initializer!")
    }
    // 反初始化器
    deinit {
        print("I'm going away!")
    }
}

var example : InitAndDeinitExample?
// 使用指定的初始化器
example = InitAndDeinitExample() // 输出"I've been created!"
example = nil // 输出"I'm going away"
// 使用便捷初始化器
example = InitAndDeinitExample(text: "Hello")
// 输出"I've been created!"
// 然后输出"I was called with the convenience initializer"
```

创建一个可以返回 nil 的初始化器(也称为可以失败的初始化器),就在 init 关键字的后面放上一个问号,并在初始化器确定它不能成功地构造该对象时,使用 return nil:

```
convenience init? (value: Int) {
    self.init()
    if value > 5 {
        // 不能初始化这个对象;返回nil,表示初始化失败 return nil
    } }
```

在使用一个可以失败的初始化器时,任何可以在其中存储该结果的变量都是可选的:

```
let failableExample = InitAndDeinitExample(value: 6)
// = nil
```

### 访问控制

在将一个方法或属性声明为 public 时,App 中的所有人都能看到它:

```
// 可供所有人访问
public var publicProperty = 123

//如果将一个方法或属性声明为 private,那只能在声明它的源文件内部看到它:
// 只能在这个源文件中访问
private var privateProperty = 123

// 仅能供本模块访问
// 这里的'internal'是默认的,可以省略
internal var internalProperty = 123
```

## 对象

### 单例模式

```swift
import UIKit

class DataCenter: NSObject {
    let dataCenterObj:DataCenter = DataCenter()
    func getDataCenter() ->DataCenter {
        return dataCenterObj
    }
}
```

### 运算符重载

类似 C++的运算符重载

```swift
class Vector2D {
    var x : Float = 0.0
    var y : Float = 0.0
    init (x : Float, y: Float) {
        self.x = x
        self.y = y
    }

}
func +(left : Vector2D, right: Vector2D) -> Vector2D {
    let result = Vector2D(x: left.x + right.x, y: left.y + right.y)
    return result
}

let first = Vector2D(x: 2, y: 2)
let second = Vector2D(x: 4, y: 1)
let result = first + second
```

## 继承

要重写一个函数,要在子类中重新声明它,并添加 override 关键字

```swift
class Car: Vehicle {
	// 继承类可以重写函数
  override func description() -> String {
  	var description = super.description()
  	return description + ", which is a car"
} }
```

在一个被重写的函数中,可以通过 super 回调该函数在父类中的版本

```swift
override func description() -> String {
         var description = super.description()
         return description + ", which is a car"
}
```

## 协议

使用协议的好处是,可以利用 Swift 的类型体系来引用任何遵守某一给定协议的对象，个人现在理解为是 Interface 概念。

```
protocol Blinking{
    var isBlinking:Bool{get}
    var blinkSpeed: Double { get set }
    func startBlinking(blinkSpeed: Double) -> Void

}

class Light:Blinking{
    var isBlinking = false
    var blinkSpeed = 1.2
    func startBlinking(blinkSpeed: Double) {
            print("now my speed is \(self.blinkSpeed)")
    }

}
```

## 扩展

```
 extension Int {
         var doubled : Int {
             return self * 2
         }
         func multiplyWith(anotherNumber: Int) -> Int {
             return self * anotherNumber
} }

2.doubled  // = 4
4.multiplyWith(32) // = 128
```

还可以利用扩展使一个类型遵守一个协议

```
extension Int : Blinking {
    var isBlinking : Bool {
        return false;
    }
    var blinkSpeed : Double {
        get {
            return 0.0; }
        set {
            // 不做任何事情
        } }
    func startBlinking(blinkSpeed : Double) {
        print("I am the integer \(self). I do not blink.")
    } }
2.isBlinking // = false
2.startBlinking(2.0) // 输出"I am the integer 2. I do not blink."
```

# 异常处理

# 变量与常量

常量和变量把一个名字(比如 maximumNumberOfLoginAttempts 或者 welcomeMessage)和一个指定类型的值(比如数字 10 或者字符串"Hello")关联起来。常量的值一旦设定就不能改变，而变量的值可以随意更改。常量和变量必须在使用前声明，用 let 来声明常量，用 var 来声明变量。下面的例子展示了如何用常量和变量来记录用户尝试登录的次数：

```swift
//基本使用
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0

//定义变量
var myVariable = 123

//定义常量
let myConstantVariable = 123

// 隐式指定整数类型
var anInteger = 2

// 明确指定整数类型
let anExplicitInteger :Int = 2
```

你可以在一行中声明多个常量或者多个变量，用逗号隔开：

```swift
var x = 0.0, y = 0.0, z = 0.0
```

常量与变量名不能包含数学符号，箭头，保留的(或者非法的)Unicode 码位，连线与制表符。也不能以数字开头，但是可以在常量与变量名的其他地方包含数字。一旦你将常量或者变量声明为确定的类型，你就不能使用相同的名字再次进行声明，或者改变其存储的值的类型。同时，你也不能将常量与变量进行互转。

### 类型标注

```
当你声明常量或者变量的时候可以加上类型标注(type annotation)，说明常量或者变量中要存储的值的类型。如果要添加类型标注，需要在常量或者变量名后面加上一个冒号和空格，然后加上类型名称。
```

#### 类型安全与类型推测

```
Swift 是一个类型安全(type safe )的语言。类型安全的语言可以让你清楚地知道代码要处理的值的类型。如果你的代码需要一个String，你绝对不可能不小心传进去一个Int。由于 Swift 是类型安全的，所以它会在编译你的代码时进行类型检查(type checks)，并把不匹配的类型标记为错误。这可以让你在开发的时候尽早发现并修复错误。当你要处理不同类型的值时，类型检查可以帮你避免错误。然而，这并不是说你每次声明常量和变量的时候都需要显式指定类型。如果你没有显式指定类型，Swift 会使用类型推测(type inference)来选择合适的类型。有了类型推测，编译器可以在编译代码的时候自动推测出表达式的类型。原理很简单，只要检查你赋的值即可。

因为有类型推测，和 C 或者 Objective-C 比起来 Swift 很少需要声明类型。常量和变量虽然需要明确类型，但是大部分工作并不需要你自己来完成。当你声明常量或者变量并赋初值的时候类型推测非常有用。当你在声明常量或者变量的时候赋给它们一个字面量(literal value或literal)即可触发类型推测。(字面量就是会直接出现在你代码中的值，比如42和3.14159。)
```

### 别名

```
类型别名(type aliases)就是给现有类型定义另一个名字。你可以使用typealias关键字来定义类型别名。当你想要给现有类型起一个更有意义的名字时，类型别名非常有用。假设你正在处理特定长度的外部资源的数据：
```

```
typealias AudioSample = UInt16
```

```
定义了一个类型别名之后，你可以在任何使用原始名的地方使用别名：
```

```
var maxAmplitudeFound = AudioSample.min // maxAmplitudeFound 现在是 0
```

```
本例中，AudioSample被定义为UInt16的一个别名。因为它是别名，AudioSample.min实际上是UInt16.min，所以会给maxAmplitudeFound赋一个初值0。
```

## 可选类型(Optional)

> - [Swift 之 ? 和 !](http://joeyio.com/ios/2014/06/04/swift---/)

```
Swift语言使用var定义变量，但和别的语言不同，Swift里不会自动给变量赋初始值，也就是说变量不会有默认值，所以要求使用变量之前必须要对其初始化。如果在使用变量之前不进行初始化就会报错：
```

```swift
var stringValue : String
//error: variable 'stringValue' used before being initialized
//let hashValue = stringValue.hashValue
let hashValue = stringValue.hashValue
```

```
Optional其实是个`enum`，里面有`None`和`Some`两种类型。其实所谓的nil就是`Optional.None`, 非nil就是`Optional.Some`, 然后会通过`Some(T)`包装(wrap)原始值，这也是为什么在使用Optional的时候要拆包(从enum里取出来原始值)的原因, 也是PlayGround会把Optional值显示为类似`{Some "hello world"}`的原因，这里是enum Optional的定义：
```

```swift
enum Optional<T> : LogicValue, Reflectable {
    case None
    case Some(T)
    init()
    init(_ some: T)

    /// Allow use in a Boolean context.
    func getLogicValue() -> Bool

    /// Haskell's fmap, which was mis-named
    func map<U>(f: (T) -> U) -> U?
    func getMirror() -> Mirror
}
```

声明为 Optional 只需要在类型后面**紧跟**一个`?`即可。如:

```
var strValue: String?   //?相当于下面这种写法的语法糖
var strValue: Optional<String>
```

> 上面这个 Optional 的声明，意思不是”我声明了一个 Optional 的 String 值”, 而是”我声明了一个 Optional 类型值，它可能包含一个 String 值，也可能什么都不包含”，也就是说实际上我们声明的是 Optional 类型，而不是声明了一个 String 类型，这一点需要铭记在心。

```
一旦声明为Optional的，如果不显式的赋值就会有个默认值nil。判断一个Optional的值是否有值，可以用if来判断：
```

```
if strValue {
    //do sth with strValue
}
```

```
注意，一旦声明为可选类型，就不再是原来的普通类型了，虽然只是简单的加了个?。对于Optional值，不能直接进行操作，否则会报错：
```

```
//error: 'String?' does not have a member named 'hashValue'
//let hashValue = strValue.hashValue
//                ^        ~~~~~~~~~

let hashValue = strValue.hashValue
```

```
如果需要获取到可选类型中的值，就要用到了!表达式：
```

```swift
let hashValue = strValue!.hashValue
```

#### 可选类型用于 Protocol 可选方法

#### 可选类型用于未实例化控件

```
考虑下这一种情况，我们有一个自定义的`MyViewController`类，类中有一个属性是`myLabel`，myLabel是在viewDidLoad中进行初始化。因为是在viewDidLoad中初始化，所以不能直接声明为普通值：`var myLabel : UILabel`，因为非Optional的变量必须在声明时或者构造器中进行初始化，但我们是想在viewDidLoad中初始化，所以就只能声明为Optional：`var myLabel: UILabel?`, 虽然我们确定在viewDidLoad中会初始化，并且在ViewController的生命周期内不会置为nil，但是在对myLabel操作时，每次依然要加上`!`来强制拆包，比如:
```

```swift
myLabel!.text = "text"
myLabel!.frame = CGRectMake(0, 0, 10, 10)
...
```

# 基本类型

## AnyObject

## 数值类型

整数就是没有小数部分的数字，比如 42 和-23。整数可以是有符号(正、负、零)或者无符号(正、零)。Swift 提供了 8，16，32 和 64 位的有符号和无符号整数类型。这些整数类型和 C 语言的命名方式很像，比如 8 位无符号整数类型是 UInt8，32 位有符号整数类型是 Int32。就像 Swift 的其他类型一样，整数类型采用大写命名法。

- **整数范围**

你可以访问不同整数类型的 min 和 max 属性来获取对应类型的最大值和最小值：

```swift
let minValue = UInt8.min  // minValue 为 0，是 UInt8 类型的最小值 let maxValue = UInt8.max  // maxValue 为 255，是 UInt8 类型的最大值
```

| 类型   | 长度                                                                                                                                | 说明                                                                                                                                                                                                                                                           |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Int    | -2147483648~2147483647                                                                                                              |                                                                                                                                                                                                                                                                |
| UInt   |                                                                                                                                     | 注意：尽量不要使用 UInt，除非你真的需要存储一个和当前平台原生字长相同的无符号整数。除了这种情况，最好使用 Int，即使你要存储的值已知是非负的。统一使用 Int 可以提高代码的可复用性，避免不同类型数字之间的转换，并且匹配数字的类型推测，请参考类型安全和类型推测 |
| 浮点数 | Double 表示 64 位浮点数。当你需要存储很大或者很高精度的浮点数时请使用此类型。Float 表示 32 位浮点数。精度要求不高的话可以使用此类型 | Double 精确度很高，至少有 15 位数字，而 Float 最少只有 6 位数字。选择哪个类型取决于你的代码需要处理的值的范围                                                                                                                                                  |

### 随机数

### 科学计算

### 类型转换

## 布尔类型

```
Swift 有一个基本的布尔(Boolean)类型，叫做Bool。布尔值指逻辑上的(logical)，因为它们只能是真或者假。Swift 有两个布尔常量，true和false：
```

```
let orangesAreOrange = true let turnipsAreDelicious = false
```

```
orangesAreOrange和turnipsAreDelicious的类型会被推测为Bool，因为它们的初值是布尔字面量。就像之前提到的Int和Double一样，如果你创建变量的时候给它们赋值true或者false，那你不需要将常量或者变量声明为Bool类型。初始化常量或者变量的时候如果所赋的值类型已知，就可以触发类型推测，这让 Swift 代码更加简洁并且可读性更高。

当你编写条件语句比如if语句的时候，布尔值非常有用：
```

```swift
    if turnipsAreDelicious {
        println("Mmm, tasty turnips!")
    } else {
        println("Eww, turnips are horrible.")
    }
    // 输出 "Eww, turnips are horrible."
```

条件语句，例如 if，请参考控制流。如果你在需要使用 Bool 类型的地方使用了非布尔值，Swift 的类型安全机制会报错。下面的例子会报告一个编译时错误：

```
let i = 1 if i {     // 这个例子不会通过编译，会报错 }
```

然而，下面的例子是合法的：

```
let i = 1 if i == 1 {     // 这个例子会编译成功 }
```

```
i == 1的比较结果是Bool类型，所以第二个例子可以通过类型检查。类似i == 1这样的比较，请参考基本操作符。和 Swift 中的其他类型安全的例子一样，这个方法可以避免错误并保证这块代码的意图总是清晰的。
```

## 空类型

## 时间日期

### NSDate

在 Objective-C 中，可以使用如下的代码创建一个 UTC 的时间：

```
NSDate *currentUTCDate = [NSDate date]
```

但是在 Swift 中，如果使用如下方式：

```
let date = NSDate()
```

获取到的会是本地时间。

#### UTC 时间与本地化时间

```swift
import UIKit

let date = NSDate();
// "Apr 1, 2015, 8:53 AM" <-- local without seconds

var formatter = NSDateFormatter();
formatter.dateFormat = "yyyy-MM-dd HH:mm:ss ZZZ";
let defaultTimeZoneStr = formatter.stringFromDate(date);
// "2015-04-01 08:52:00 -0400" <-- same date, local, but with seconds
formatter.timeZone = NSTimeZone(abbreviation: "UTC");
let utcTimeZoneStr = formatter.stringFromDate(date);
// "2015-04-01 12:52:00 +0000" <-- same date, now in UTC
```

#### 时间比较

如果需要比较两个日期，可以使用如下方法，在如下代码中已经展示了如何处理不同的返回结果：

```swift
// Date comparision to compare current date and end date.
var dateComparisionResult:NSComparisonResult = NSDate().compare(endDate)

if dateComparisionResult == NSComparisonResult.OrderedAscending
{
    // Current date is smaller than end date.
}
else if dateComparisionResult == NSComparisonResult.OrderedDescending
{
    // Current date is greater than end date.
}
else if dateComparisionResult == NSComparisonResult.OrderedSame
{
    // Current date and end date are same.
}
```

#### TimeStamp

如果需要将某个 TimeStamp("/Date(1427909016000-0800)”)转化为 NSDate 对象，那么可以使用如下的扩展工具，该扩展将会把 TimeStamp 转化为本地化时间。其中 1427909016000 表示从 Unix 计时以来的毫秒数，而-0800 表示时区：

```swift
extension NSDate {
    convenience init?(jsonDate: String) {
        let prefix = "/Date("
        let suffix = ")/"
        let scanner = NSScanner(string: jsonDate)

        // Check prefix:
        if scanner.scanString(prefix, intoString: nil) {

            // Read milliseconds part:
            var milliseconds : Int64 = 0
            if scanner.scanLongLong(&milliseconds) {
                // Milliseconds to seconds:
                var timeStamp = NSTimeInterval(milliseconds)/1000.0

                // Read optional timezone part:
                var timeZoneOffset : Int = 0
                if scanner.scanInteger(&timeZoneOffset) {
                    let hours = timeZoneOffset / 100
                    let minutes = timeZoneOffset % 100
                    // Adjust timestamp according to timezone:
                    timeStamp += NSTimeInterval(3600 * hours + 60 * minutes)
                }

                // Check suffix:
                if scanner.scanString(suffix, intoString: nil) {
                    // Success! Create NSDate and return.
                    self.init(timeIntervalSince1970: timeStamp)
                    return
                }
            }
        }

        // Wrong format, return nil. (The compiler requires us to
        // do an initialization first.)
        self.init(timeIntervalSince1970: 0)
        return nil
    }
}
```

使用的例子如下：

```swift
if let theDate = NSDate(jsonDate: "/Date(1427909016000-0800)/")
{
    println(theDate)
}
else
{
    println("wrong format")
}
```

### NSDateFormatter：格式化时间

```swift
var dataString = "April 1, 2015" as String
var dateFormatter = NSDateFormatter()
dateFormatter.dateFormat = "MM-dd-yyyy"
dateFormatter.timeZone = NSTimeZone.localTimeZone()

// convert string into date
let dateValue = dateFormatter.dateFromString(dataString) as NSDate!

println(dateValue)
```

![](http://www.brianjcoleman.com/wp-content/uploads/2015/04/Sg0tZ.png)

### NSCalendar

```swift
// Playground - noun: a place where people can play

import UIKit

// Setup the calendar object
let calendar = NSCalendar.currentCalendar()

// Set up date object
let date = NSDate()

// Create an NSDate for the first and last day of the month
//let components = calendar.components(NSCalendarUnit.CalendarUnitYear |
//                                     NSCalendarUnit.CalendarUnitMonth |
//                                     NSCalendarUnit.WeekdayCalendarUnit |
//                                     NSCalendarUnit.WeekCalendarUnit |
//                                     NSCalendarUnit.CalendarUnitDay,
//                                     fromDate: date)

// Create an NSDate for the first and last day of the month
let components = NSCalendar.currentCalendar().components(NSCalendarUnit.CalendarUnitMonth, fromDate: date)


components.month

// Getting the First and Last date of the month
components.day = 1
let firstDateOfMonth: NSDate = calendar.dateFromComponents(components)!

components.month  += 1
components.day     = 0
let lastDateOfMonth: NSDate = calendar.dateFromComponents(components)!

var unitFlags = NSCalendarUnit.WeekOfMonthCalendarUnit |
                NSCalendarUnit.WeekdayCalendarUnit     |
                NSCalendarUnit.CalendarUnitDay

let firstDateComponents = calendar.components(unitFlags, fromDate: firstDateOfMonth)
let lastDateComponents  = calendar.components(unitFlags, fromDate: lastDateOfMonth)

// Sun = 1, Sat = 7
let firstWeek = firstDateComponents.weekOfMonth
let lastWeek  = lastDateComponents.weekOfMonth

let numOfDatesToPrepend = firstDateComponents.weekday - 1
let numOfDatesToAppend  = 7 - lastDateComponents.weekday + (6 - lastDateComponents.weekOfMonth) * 7

let startDate: NSDate = calendar.dateByAddingUnit(NSCalendarUnit.CalendarUnitDay, value: -numOfDatesToPrepend, toDate: firstDateOfMonth, options: nil)!
let endDate:   NSDate = calendar.dateByAddingUnit(NSCalendarUnit.CalendarUnitDay, value: numOfDatesToAppend, toDate: lastDateOfMonth, options: nil)!

Array(map(0..<42) {
    calendar.dateByAddingUnit(NSCalendarUnit.CalendarUnitDay, value: $0, toDate: startDate, options: nil)!
})

"\(components.year)"


var dateString = "2014-10-3" // change to your date format
var dateFormatter = NSDateFormatter()
dateFormatter.dateFormat = "YYYY-MM-dd"

var someDate = dateFormatter.dateFromString(dateString)
println(someDate)
```

# 字符串

```swift
  let string1 : String = "Hello"
     let string2 : String = "Hel" + "lo"
     if string1 == string2 {
         println("The strings are equal")
  }
```

## 创建增删

### 字符串插值

Swift 用字符串插值(string interpolation)的方式把常量名或者变量名当做占位符加入到长字符串中，Swift 会用当前常量或变量的值替换这些占位符。将常量或变量名放入圆括号中，并在开括号前使用反斜杠将其转义：

```swift
println("The current value of friendlyWelcome is \(friendlyWelcome)")
// 输出 "The current value of friendlyWelcome is Bonjour!
```

## 索引遍历

### 存在判断

```
 if string1.hasPrefix("H") {
         println("String begins with an H")
 }
if string1.hasSuffix("llo") {
         println("String ends in 'llo'")
}
```

## 类型编码

### 编解码

```swift
let stringToConvert = "Hello, Swift"
let data = stringToConvert.dataUsingEncoding(NSUTF8StringEncoding)
```

# Indexed Collections

## 数组(Array)

```
var arrayOfIntegers : [Int] = [1,2,3]
// 隐式指定
var implicitArrayOfIntegers = [1,2,3]

// 也可以创建空数组,但必须提供其类型
let anotherArray = [Int]()

//使用 append 函数向数组的末尾追加对象
myArray.append(4)

//数组中的任意位置插入对象
myArray.insert(5, atIndex: 0)
```

## 元组(Tuples)

元组(tuples)把多个值组合成一个复合值。元组内的值可以使任意类型，并不要求是相同类型。下面这个例子中，(404, "Not Found")是一个描述 HTTP 状态码(HTTP status code)的元组。HTTP 状态码是当你请求网页的时候 web 服务器返回的一个特殊值。如果你请求的网页不存在就会返回一个 404 Not Found 状态码。

```swift
let http404Error = (404, "Not Found")
// http404Error 的类型是 (Int, String)，值是 (404, "Not Found")
```

(404, "Not Found")元组把一个 Int 值和一个 String 值组合起来表示 HTTP 状态码的两个部分：一个数字和一个人类可读的描述。这个元组可以被描述为“一个类型为(Int, String)的元组”。你可以把任意顺序的类型组合成一个元组，这个元组可以包含所有类型。只要你想，你可以创建一个类型为(Int, Int, Int)或者(String, Bool)或者其他任何你想要的组合的元组。

你可以将一个元组的内容分解(decompose)成单独的常量和变量，然后你就可以正常使用它们了：

```
let (statusCode, statusMessage) = http404Error
println("The status code is \(statusCode)")
// 输出 "The status code is 404"
println("The status message is \(statusMessage)")
// 输出 "The status message is Not Found"
```

如果你只需要一部分元组值，分解的时候可以把要忽略的部分用下划线(\_)标记：

```swift
let (justTheStatusCode, _) = http404Error
println("The status code is \(justTheStatusCode)")
// 输出 "The status code is 404"
```

### 索引遍历

你还可以通过下标来访问元组中的单个元素，下标从零开始：

```
println("The status code is \(http404Error.0)")
// 输出 "The status code is 404"
println("The status message is \(http404Error.1)")
// 输出 "The status message is Not Found"
```

你可以在定义元组的时候给单个元素命名：

```
let http200Status = (statusCode: 200, description: "OK")
```

给元组中的元素命名后，你可以通过名字来获取这些元素的值：

```swift
println("The status code is \(http200Status.statusCode)")
// 输出 "The status code is 200"
println("The status message is \(http200Status.description)")
// 输出 "The status message is OK"
```

作为函数返回值时，元组非常有用。一个用来获取网页的函数可能会返回一个(Int, String)元组来描述是否获取成功。和只能返回一个类型的值比较起来，一个包含两个不同类型值的元组可以让函数的返回信息更有用。请参考[函数参数与返回值(06_Functions.html#Function_Parameters_and_Return_Values)。注意：元组在临时组织值的时候很有用，但是并不适合创建复杂的数据结构。如果你的数据结构并不是临时使用，请使用类或者结构体而不是元组。请参考类和结构体。

# Keyed Collections

## 字典

字典是一种将键映射到值的类型，类似 Java 的 Map,PHP 的数组

```
 var crew = [
          "Caption": "Jean-Luc Picard",
          "First officer": "William Riker",
          "Second Officer": "Data"
];


crew["Captain"]
// = "Jean-Luc Picard"
```
