---
title: Swift学习(1)
date: 2017-09-10 09:35:31
tags: Swift
categories: Swift
---

<blockquote>简单高效</endblockquote>

## Swift基础部分

包含的内容:

* 常量和变量
* 注释
* 分号
* 整数
* 浮点数
* 类型安全和类型推断
* 数值型字面量
* 数值型类型转换
* 类型别名
* 布尔值
* 元组
* 可选
* 断言

Swift包含了C和Objective-C上所有基础数据类型，Int表示整形值；Double和Float表示浮点值；Bool是布尔类型值；String是文本类型数据。Swift还提供了三个基本的集合类型，Array，Set和Dictionary。

如同C语言一般，Swift使用变量来进行存储并通过变量名来联值。在Swift中，广泛的使用着值不可变的变量，它们就是常量，而且比C语言的常量更强大。在Swift中，如果你要处理的值不需要改变，那使用常量可以让你的代码更加安全并且更清晰的表达你的意图。

除了我们熟悉的类型，Swift还增加了Objective-C中没有的高阶数据类型比如元组（Tuple）。元组可以让你创建或者传递一组数据，比如作为函数的返回值时，你可以用一个元组返回多个值。

Swift还增加了可选（Optional）类型，用于处理值缺失的情况。可选表示“那儿有一个值，并且它等于x“或者”那儿没有值“。可选有点像在Objective-C中nil，但是它可以用在任何类型上，不仅仅是类。可选类型Objective-C中的nil指针更加安全也更具表现力，它是Swift许多强大特性的重要组成部分。

Swift是一门类型安全的语言，可选类型就是一个很好的例子。Swift可以让你清楚地知道值的类型。如果你的代码期望得到一个String，类型安全会阻止你不小心传入一个Int。你可以在开发阶段尽早发现病避免错误。

### 常量和变量

声明常量和变量

常量和变量使用之前必须先声明，用let来声明常量，用var来声明来声明变量。下面的例子记录用户尝试登录的次数。

``` bash
let max=10
var index=0
```
这两行代码可以被理解为：

“声明一个名字是max的新常量，并给它一个值10.然后，声明一个变量是index给它初始化一个值时0.“

你可以在一行中声明多个常量或者变量，用逗号隔开：
``` bash
var x=0.0,y=0.0,z=0.0
```
注意：
如果你的代码中不需要改变的值，请使用let关键字将它声明为常量。需要改变的量声明为变量

### 类型标注

当你声明常量或者变量的时候可以加上类型标注（type annotation），说明常量或者变量中要存储的值的类型。如果要添加类型标注，需要在常量或者变量名后面加上冒号和空格，然后加上类型名称。
举例如下：

``` bash
var message:String
```
声明中的冒号代表是...类型，所以这行代码可以被理解为：
”声明一个类型为String，名字为message的变量。“
”类型为String“的意思是”可以存储任意String类型的值。“

注意：
一般来说你很少需要写类型标注。如果你在声明常量或者变量的时候赋予了一个初始值，Swift可以推断出这个常量或者变量的类型，请参考类型安全和类型推断。在上面的例子中，message没有赋予初始值，所以变量需要通过一个类型标注指定的，而不是通过初始值推断的。
### 常量和变量的命名

你可以用任何你喜欢的符号作为变量和常量名，包括Unicode字符：
``` bash
let 你好="你好世界"
```
常量与变量名不能包含数学符号，箭头，保留的（或者非法的）Unicode码位，连线与制表符。也不能以数字开头，但是可以在常量与变量名的其他地方包含数字。
一旦你将常量或者变量声明为确定的类型，你就不能使用相同的名字再次进行声明，或者改变其存储类型。同时，你也不能讲常量与变量相互转换。

### 输出常量和变量

你可以用prinln函数来输出当前常量或者变量的值：
``` bash
println(friend)
```
println是一个用来输出全局函数，输出的内容会在最后换行，如果你用Xcode，println将会将输出内容打印到”console“面板上。（另一个函数叫print，唯一区别在输出内容最后是不会换行的。）

println函数输出传入的String值：
``` bash
println("this is a string")
//输出 “this is  a string”
```
与Cocoa里的NSLog函数类似的是，println函数可以输出更复杂的信息。这些信息可以包含当前的变量的值。

Switf用字符串插值（string interpolation）的方式将常量名或者变量名当作占位符加入到长字符串中，会用当前变量或者常量来替换这些占位符。将常量或者边领放入圆括号中，并在括号前使用反斜杠将其转义；
``` bash
println("The current value of friend is \(friend)")
//输出 "The current value of friend is xiaoming "
```

### 注释
请将你的代码中非执行文本注释成提示或者笔记以便你将来阅读。Swift的编译器将会在编译代码时自动忽略掉注释部分。
Swift中的注释与c语言的注释非常的相似。单行注释以双正斜杠（//）作为标记：
``` bash
//这是一个注释
```
你也可以使用多行注释，其起始标记为正斜杠后加一个星号,终止标记为一个星号后加蛋哥正斜杠
``` bash
/*这是一个
多行的注释*/
```
### 分号

与其他大部分编程语言不同，Swift并强制没一条语句的结尾加分号（；），当然，你可以按照自己的习惯加分号。有一种情况必须使用分号，即你打算在同一行内写出多条独立语句。

### 整数
整数就是没有小数部分的数字，比如42和-12.整数可以是用符号（正负零）

Swift提供了8，16，32，64位的有符号和无符号整数类型。这些整数类型和c语言的命名方式很像，比如无符号整数类型是UInt8，32位有符号类型是Int32.就像Swift的其他类型一样，整数类型采用大些命名法。

### 整数范围
你可以访问不同整数类型的min和max属性来获取对应类型的最大值和最小值：
``` bash
let minValue=UInt8.min //minValue为0，是UInt8类型的最小值
let maxValue=UInt8.max//maxValue为255,是Uint8类型的最大值
```

### Int
一般来说，你不需要专门指定整数的长度。Swift提供了一个特殊的数据类型Int，长度与原生平台相同：
* 在32位平台上，Int和Int32位长度相同
* 在64位平台上，Int和Int64位长度相同
除非你需要特定长度的整数，一般来说使用Int就够了。着可以提高代码的一致性风格和复用性。即使在32位平台上，Int可以存储的整数范围也可以达到-2147483648～2147483647，大多数时候已经足够了。

UInt
Swift也提供了一个特殊的无符号类型UInt，长度与当前平台的原生字长相同：
* 在32位平台上，UInt和UInt32位长度相同
* 在64位平台上，UInt和UInt64位长度相同

### 类型安全和类型推断
Swift是一个类型安全的语言。类型安全的语言可以让你清楚地知道代码要处理值的类型。如果你的代码是需要一个String，你绝对不可能不小心穿进去一个Int。

由于Swift是类型安全的，所以它会在编译你的代码时进行类型检查（type check），并把不匹配的类型标记为错误。着可以让你在开发的时候尽早的发现并修复错误。

当你处理不同类型的值时，类型检查可以帮你避免错误。然而，这并不是说每次声明常量和变量的时候都需要显式指定类型。如果你没有显式追定类型，Swift会使用类型推断来选择合适的类型。有了类型推断，编译器可以在编译代码的时候自动推断出表达式的类型。原理很简单，只要检查你赋予的值即可。

因为有了类型推断，和C或者Objective-C比起来Swift很少需要类型声明。常量和变量虽然需要明确类型，但是大部分工作不需要你自己来完成。

当你声明常量或者变量并赋予初值的时候类型推断非常有用，当你在声明常量或者变量的时候给他们一个初始值即可出发类型推断。
例如，如果你给一个常量赋予值42并且没有表明类型，Swift可以推断出常量的类型Int，因为你的初始值看起来像一个整数：
``` bash
 let number=42
 /// number 会被推测为Int类型
```

同理，如果你没有给浮点字面标明类型，Swift会推断出你想要的是double：
``` bash
let pi=3.141596
//pi会被推测出为double类型的
```
当推断浮点数的类型时，Swift总是会选择Double而不是Float。
如果表达式中同时出现了整数和浮点数，会被推断出Double类型：

``` bash
let pis=3+0.14159
// pis会被推测为Double
```
原始值3没有显式声明类型，而表达式中出现了一个浮点字面量，所以表达式会被推断为Double

### 数值型字面量
整数字面量可以被写作：

* 一个十进制的，没有前缀
* 一个二进制的，前缀是0b
* 一个八进制的，前缀是0o
* 一个十六进制的，前缀是0x

下面的所有整数字面量的十进制值都是17

``` bash 
let number1=17      
let number2=0b10001  //二进制的17
let number3=0o21    //八进制的17
let number4=0x11    //十六进制的17
```
浮点字面量可以是十进制（无前缀）或者以是十六进制的（有前缀）。小数点两边必须至少有一个十进制数字（或者是十六进制的数字）。浮点字面量还有一个可选的指数（exponent），在十进制浮点数中通过大写或者小写的e来指定，在十六进制浮点数中通过大些或者小写的p来指定。
如果一个十进制的指数为exp，那这个数相当于技术和10^exp的乘积的乘积：
* 1.25e2 表示 1.25 × 10^2，等于 125.0。

* 1.25e-2 表示 1.25 × 10^-2，等于 0.0125。

如果一个十六进制数的指数为exp，那这个数相当于基数和2^exp的乘积：
* 0xFp2 表示 15 × 2^2，等于 60.0。
* 0xFp-2 表示 15 × 2^-2，等于 3.75。
下面的这些浮点字面量都等于十进制的12.1875:
``` bash
 let number1=12.1875
 let number2=1.21875e1
 let number3=0xC.3p0
```
数值类字面量可以包括额外的格式来增强可读性。整数和浮点数可以添加额外的零并且包含下划线，并不会影响字面量：
``` bash
 let number1=000123.456
 let number2=1_000_000
 let number3=1_000_000.000_000_1
```
### 数值型类型转换
通常来讲，即使代码中的整数常量和变量已知非负，也请使用Int类型。总是使用默认的整数类型可以保证你的整数常量和变量可以直接被复用并且可以匹配整数数字字面量的类型推断。只有在必要的时候才使用其他整数类型，比如要处理外部的长度明确的数据或者为了优化性能，内存占用等等。使用显式指定长度的类型及时发现值溢出并且可以暗示正在处理的特殊数据。
### 整数转换
不同整数类型的变量和常量可以存储不同范围的数字。Int8类型的常量或者变量可以存储的数字范围为-128～127，而UInt8类型的常量或者变量能存储的数字范围是0～255.如果数字超出了存储的范围，编译的时候会报错：
``` bash
    let number1:UInt8=-1
    //Uint8 类型不能存储负数，所以会报错
    let number2:Int8=Int8.max+1
    //Int8 类型不能存储超过最大值的数，所以会报错
```
由于每种整数类型都可以存储不同范围的值，所以你必须根据不同情况选择性使用数值型类型转换。这种选择性使用的方式，可以预防隐式转换的错误并让你的代码中的额类型转换意图变得清晰。

要讲一种数字类型转换成另一种，你要讲当前值来初始化一个期望类型的新数字，这个数字的类型就是你的目标类型。在下面的例子中，常量 number 是UInt16类型，然而常量number1时UInt8类型。它们不能直接相加，因为它们类型不同。所以要调用UInt16（number1）来创建一个新的UInt16数字并用number1的值来初始化，然后使用这个新数字来计算：
``` bash
let number:UInt16=2_000
let number1:UInt8=1
let sub=number+UInt16(number1)

```

### 整数和浮点数转换
整数和浮点数的转换必须显式指定类型：

``` bash
    let three=3
    let number1=0.14159
    let pi=Double(three)+number1
```
这个例子中，常量three的值被用来创建一个double类型的值，所以加号两边的数类型必须相同，如果不进行转换，两者无法相加。
浮点数到整数的反向转换同样行，整数类型可以用Double或者float了型来初始化：
``` bash
    let intPi=Int(pi)
```
当用这种方式来初始化一个新的数值时，浮点值会被截断。也就是说4.75会变成4，-3.9会变成3.

### 类型别名
类型别名（type aliases）就是给所有类型定义另一个名字。你可以使用typealias关键字来定义别名。

当你想要给现有的类型起一个更有意义的名字时，类型别名非常有用。假设你正在处理特定长度的外部资源的数据：

``` bash
   typealias AudioSample=UInt16
```
当你定义了一个别名之后，你可以在任何使用原始名的地方使用别名：
``` bash

var min=AudioSample.min
//min现在的值时0
```
本例中，AudioSample被定义为UInt16的一个别名。因为它时别名，AudioSample.min实际上就是UInt16.min所以会给min赋予一个初值为0。
### 布尔值
Swift有一个基本的布尔（Boolean）累心，叫做Bool。布尔值指逻辑上的，因此它们只能时真或假。Swift有两个布尔常量，true和false

### 元组
元组（tuples）把多个值组合成一个复合值。元组内的值可以是任意类型，并不是要求相同类型。

下面这个例子中，（4004，“Not Found”）是一个描述HTTP状态码（Http status code）的元组。

``` bash
    let http404Error=(404,"Not Found")
```
(404,"Not Found")元组把一个Int值和一个String值组合起来表示Http状态码的两个部分：一个数字和一个人类可读的描述。这个元组可以被描述为“一个类型为（Int，String）的元组”。
你可以把任意顺序的类型组成一个元组，这个元组可以包含所有类型。只要你想，你可以创建一个类型为（Int，Int，Int）或者（String，Bool）或者其他任何你想要的组合的元组。
你可以将一个元组的内容分解为单独的常量和变量，然后你可以正常使用它们了：
``` bash
    let(statusCode,statusMessage)=http404Error
    println("The status code is \(statusCode)")
    //输出 “The status code is 404”
    println（“The status message is\(statusMessage)”）
    //输出 “The status message is Not Found”
```
如果你只需要一部分元组值，分解的时候可以把忽略的部分用下划线（_）标记:
``` bash
 let(code,_)=http404Error
 println("The status code is \(code)")
 //输出“The status code is 404”
```

此外，你还可以通过下标来访问元组中的单个元素，下标从零开始：
``` bash
    println("The status code is \(http404Error.0)")
    //输出"The status code is 404"
    println("The status message is \(http404Erroe.1)")
    //输出"The status message is Not Found"
```
你可以在定义元组的时候给单个元素命名：
``` bash
    let http200Status=(statusCode:200,description:"0k")
```
给元组中的元素命名之后，你可以通过名字来获取这些元素的值：
``` bash
 println("The status code is \(http200Status.statusCode)")
//输出"The status code is 200"
 println("The status message is \(http200Status.description)")
//输出"The status message is ok"
```
作为函数返回值时，元组非常有用。一个用来获取网页的函数可能会返回一个（int,String)类型来获取成功。和只能返回一个类型的值比起来，一个包含两个不同类型的元组可以让函数的返回信息更有用。

### 可选类型
使用可选类型（optionals）来处理可能缺少的情况。
下面的例子使用toInt方法来尝试将一个string转换成Int：
``` bash
let possibleNumber="123"
let convertNumber=possibleNumber.toInt()
```
因为toInt方法可能会失败，所以它返回一个可选类型Int，而不是Int。一个可选的Int被写作Int？而不是Int。问号暗示包含的值时可选类型，也就是说可能包含Int也可能不包含。

### if语句以及强制解析
你可以使用if语句来判断一个可选时否包含值。如果可选类型有值，结果时ture；如果没有值结果时false。
当你确定可选类型确实包含值之后，你可以在可选的名字后面加一个感叹号（！）来获取值。
``` bash
 if(convertedNumber!=nil){
    println("\(possibleNumber) has an integer value of \(convertedNumber)")
}else{
println("\(possibleNumber) could not be converted to an Integer")

}

```

### 可选绑定
使用可选绑定（optional binding）来判断可选类型是否包含值，如果包含就把值赋予给一个临时变量或者变量。可选绑定可以用在if和while语句中来对可选类型的值进行判断在把值赋给一个常量或者变量。if和while语句，请参考控制流。
向下面这样在if语句中写一个可选绑定：
``` bash
    if let actuaNumber=possibleNumber.toInt(){
        println("\(possbilenumber) has an integer value of \()actualNumber")
    }else{
        println("\(possiblenumber) could not be converted to an integer")
    }
```

### nil
你可以给可选变量赋值为nil来表示它没有值：

``` bash
    var serverResponseCode: Int?=404
// severResponseCode 包含一个可选的Int值404
serverResponseCode=nil
//serverResponseCode 现在不包含值
```
如果你声明一个可选常量或者变量但是没有赋值，它们会自动被设置为nil：

``` bash
    var surveyAnswer:String?
// surveyAnswer 被自动设置nil
```

### 隐式解析可选类型
如上所述，可选类型暗示了常量或者变量可“没有值”。可选可以通过if语句来判断是否有值，如果有值的话可以通过可选绑定来解析值。
一个隐式解析可选类型其实就是一个普通的可选类型，但可以被当作非可选类型来使用，并不需要每次都使用解析






