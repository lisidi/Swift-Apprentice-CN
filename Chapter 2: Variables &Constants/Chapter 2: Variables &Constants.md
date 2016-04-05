# Chapter 2: Variables &Constants 变量和常量

[TOC]

现在，你知道计算机如何解释你编写的代码，以及你需要用什么工具来编写，是时候开始学习关于 Swift 本身的知识了。

在这一章，你会发现常量、 变量、 类型和元组，并学习如何声明它们、 命名它们和更改它们。你还将了解类型推导，Swift的最重要特征之一，使你的编码容易得多。

## Naming data 命名数据

简单来说，计算机编程就是操作数据。请记住，你在屏幕上看到的一切都可以简化成数字发送给 CPU 。有时你处理的数据是各种类型的数字，但还有时数据可能是更复杂的形式，如文本、 图像和集合。

在 Swift 代码中，你可以给每条数据命名，作为以后来引用。名字要与他的数据类型相关，比如：text ，a date, numbers 。

在这一章，你将了解一些基本的类型，还有其它的类型在本书的剩余部分。

#### Constants 常量

看看这本书的第一位:

``` 
let number: Int = 10
```

声明一个常量number，类型为 Int，然后给它赋值10。

Int 类型只能够存储整数，所以也有一个方式去存储小数。

例如:

``` 
let pi: Double = 3.14159
```

这和 Int 常量很相似，除了名称和类型是不同的。这次常量是 Double 类型，可以存储高精度小数。

还有一种称为Float，简称浮点数，存储的小数与Double相比精度低。Float占用内存少于Double，但一般来说，数字所占用的内存并不是一个大问题，你会看到在很地方会使用Double。

一旦你已经声明一个常量，就不能更改其数据。例如，考虑下面的代码:

``` 
let number: Int = 10
number = 0
```

代码报错：

``` 
  Cannot assign to value: 'number' is a 'let' constant
```

在Xcode中，你将会看到错误以这种方式来呈现：

 ![Snip20151117_12](http://7xoguz.com1.z0.glb.clouddn.com/b2/pngSnip20151117_12.png)

常量对于一个不可改变的值是十分有用的。例如，如果你正在模型化一架飞机，要记录座位总数，你可以使用一个常量。

你甚至可以使用常量来定义一个人的年龄。即使他们的年龄将改变，而你可能却只是关心他们在这特别时刻的年龄。

#### Variables 变量

通常您想更改名字后面的数据。例如，如果你要记录你的银行存款，你可以使用变量，而不是一个常量。

如果你的程序数据永远不会改变，那是一个相当枯燥乏味的程序!但如你所见，不可能改变一个常量的数据。

当你知道你需要修改一些数据时，你应该使用变量来表示该数据而不是用一个常量。你声明一个变量以类似的方式，就像这样:

``` 
var variableNumber: Int = 42
```

只有声明的第一部分是不同的: 你声明常量用let，而声明变量使用var。

一旦你已经声明一个变量，你可以将其随意更改为任何你想要的类型，只要该类型保持不变就行。例如，要更改上面声明的变量，你可以这样做:

``` 
var variableNumber: Int = 42
variableNumber = 0
variableNumber = 1_000_000
```

若要更改变量，您只需设置其等于新值。

``` 
注意: 在Swift中，你可以选择使用下划线来使数字变得更加可读。下划线的数量和位置由你决定。
```

这是介绍results sidebar的好时机。当你输入上面的代码到playground时，你会看到在右侧results sidebar中的每一行显示了 variableNumber 的当前值：

 ![Snip20151117_13](http://7xoguz.com1.z0.glb.clouddn.com/b2/pngSnip20151117_13.png)

results sidebar将为每一行显示一个相关的结果，如果代码结果存在的话。至于变量或常量，右侧的结果都是个新值，不管你是声明的常量，或声明变量或重新分配的变量。

#### Naming 命名

为你的变量和常量总是尽量选择有意义的名称。

一个好名字能够具体描述变量或常量。这里是一些好名字:

- personAge
- numberOfPeople
- gradePointAverage

通常一个不好的名字描述性不强。下面是一些不好的名字:

- a
- temp
- average

关键是要确保你再一次读代码，就会明白这些变量或常量指代的是什么。不要错误地认为你有可靠的记忆力! 在计算机编程中，过一两天再回头看以前的代码，却忘记了很多东西，这是很常见的。为你自己变得更轻松，你应该给你的变量和常量一个直观、 精确的名字。

在Swift中，你甚至可以使用Unicode 字符的完全范围 。这意味着你可以这样声明一个变量:![Snip20151117_14](http://7xoguz.com1.z0.glb.clouddn.com/b2/pngSnip20151117_14.png)

这可能会让你笑，但使用谨慎地使用这些特殊字符。他们很难输入并可能会让你更痛苦。![Snip20151117_15](http://7xoguz.com1.z0.glb.clouddn.com/b2/pngSnip20151117_15.png)

像这些特殊字符可能比 Swift 代码会产生更多感觉;  你将学习更多关于 Unicode 在第 4 篇，"Strings"。

#### Type conversion 类型转换

有时你想将数据的格式。幼稚的方式会像这样:

``` 
var integer: Int = 100
var decimal: Double = 12.5
integer = decimal
```

这样做Swift会编译报错：

``` 
Cannot assign a value of type 'Double' to a value of type 'Int'
```

有些编程语言可能不是很严格，将会自动执行这样的数值转换。然而，Swift关于类型方面是非常严格的，你不能随意分配一种类型的值给另一种类型的变量。

记住，计算机是依赖于程序员的操作。在Swift中，类型的转换要显式。

你需要显式地告知你想要转换的类型，而不是仅仅赋值：

``` 
var integer: Int = 100
var decimal: Double = 12.5
integer = Int(decimal)
```

``` 
注意: 在这种情况下，分配的小数到整数，精度会损失: 整数变量integer是12而不是12.5。这就是显式的重要性。Swift 想要确保你知道你在做什么，并且通过执行类型转换你可能最终会丢失数据。
```

#### Mini-exercises 迷你练习

如果你还没有自己独自使用Xcode编码，现在就是时候创建一个新的playground来做一些练习。

1.声明一个Int类型的常量myAge，并给其赋值你的年龄。

2.声明一个Double类型的变量averageAge。初始化，给其赋myAge值；你需要使用显式类型转换做到这一点。然后，然后给其赋值，值为你得年龄和我的年龄的平均数。通过你自己的脑算就行—在接下来得篇章你会使用Swift计算。



## Tuples 元组

有时数据是成对或者三个一副。一个例子就是是一对 (x，y) 平面坐标。同样，一套 3D 坐标是由 x 值、 y 值和 z 值组成。

在 Swift中，有一个非常简单的方法来表示这种相关的数据，就是通过使用一个元组。

元组这种类型表示的数据可以由多个类型的值组成。在元组里你想有几个值都行，例如，你可以定义一对 2D 坐标，其中每个轴的值是一个整数，就像这样:

``` 
let coordinates: (Int, Int) = (2, 3)
```

坐标的类型是个元组，包含两个 Int 值。元组中值的类型是Int，被逗号隔开。

你同样可以创建一个 值为Double类型的元组，如下所示:

``` 
let coordinates: (Double, Double) = (2.1, 3.5)
```

或者你可以混合匹配值的类型，继而组成的元组，如下所示:

``` 
let coordinates: (Double, Int) = (2.1, 3)
```

在这里是如何访问一个元组中的数据:

``` 
let coordinates: (Int, Int) = (2, 3)
let x: Int = coordinates.0
let y: Int = coordinates.1
```

你可以通过他们在元组中的位置来引用他们，所以在此示例中: x 等于 2 , y 将等于 3。

``` 
注意：在计算机编程中从零开始是很常见的做法，被称为第0个索引。你会在第10章“数组”中再次看到。
```

在前面的例子中，可能不是显而易见的一点就是: 第一个值，index为0 ，是x坐标。这第二个值，index为1 ，是y坐标。

这就是另一个证明, 关于为什么我们总要以一个避免混乱的方式去命名变量。

幸运的是，Swift允许你命名一个元组中的单独的一部分, 帮助你明确每一部分代表的是什么。例如:

``` 
let coordinatesNamed: (x: Int, y: Int) = (2, 3)
```

在这里，通过一个标签声明了coordinatesNamed元组中每部分的数据类型。

然后，当你想要访问元组中的每一部分时，通过名称访问它:

``` 
let x: Int = coordinatesNamed.x
let y: Int = coordinatesNamed.y

```

这更加清晰易懂。往往这也更容易去命名你的元组中的成员。

如果你想同时访问元组中的每一个成员，你还可以使用短语法来变得更轻松:

``` 
let coordinates3D: (x: Int, y: Int, z: Int) = (2, 3, 1)
let (x, y, z) = coordinates3D

```

声明3个常量并依次赋值。该代码相当以下内容:

``` 
let coordinates3D: (x: Int, y: Int, z: Int) = (2, 3, 1)
let x = coordinates3D.x
let y = coordinates3D.y
let z = coordinates3D.z

```

如果您想要省略元组中每个确定的元素，你可以用下划线替代。例如，如果你要进行2D计算，想要忽略 coordinates3D 中的 z 坐标，你可以这么写:

``` 
let (x, y, _) = coordinates3D
```

这行代码只声明 x 和 y。这个_ ，意味着你现在忽略了这一部分。

``` 
注意:现在你应该发现在Swift中你可以通过下划线 _ ,来省略一个值.
```

#### Mini-exercises 迷你练习

1.声明一个常量元组,其中包括三个Int值, 一个Double值。

并且用这个元组表示那一年那一月那一天的温度(整好4个值)。

2.通过给元组中每一部分加以相关联的名称,来改变元组。month, day, year and averageTemperature。

3.读出day和averageTemperature的值, 你需要使用_来省略month和year。

4.到现在你也只是见过常量元组, 但是你也可以创建变量元组将 let 换成 var ,来改变你在练习中创建的元组, 现在给元组中的averageTemperature赋个新值。

## Type inference 类型推导

每次看到的已经声明的常量和变量都有一个关联的类型

``` 
let coordinates3D: (x: Int, y: Int, z: Int) = (2, 3, 1)
let (x, y, z) = coordinates3D

```

第二行并没有声明x, y, z的类型为Int。那Swift是怎么知道它们是Int类型的呢？

通过读代码，很清晰地知道第二行中的3个常量是Int类型的。因为你已经声明了一个包含3个Int值得元组。

原来Swift编译器可以做到这个过程的推导。你不需要告诉这个类型—它就能自己指出来。嗯，优雅！:]

碰巧地是，除了元组你都可以省略类型。事实上，在大多数地方你都可以省略类型，因为Swift已经知道啦！

例如，考虑下面这个常量的声明：

``` 
  let typeInferredInt = 42

```

右手边的值是integer类型的。Swift也知道。因此它推断常量的类型应该是Int 。这个过程就叫做**类型推导**，这是Swift语言威力中一个关键的部分。

有时对于检查一个被推导过的变量或者常量的类型来说是很有用的。在playground中，你可以按住Option键，并点击这个变量或者常量的名字。Xcode将显示一个弹出视图：

![Snip20151118_1](http://7xoguz.com1.z0.glb.clouddn.com/b2/pngSnip20151118_1.png)

Xcode会告诉你这个被推导过的类型，它是怎么做的？它通过给你这一个声明，这个声明是“在没有其他类型的情况下，你将必须使用的”。

对于其他类型也一样：

``` 
let typeInferredDouble = 3.14159
```

再次点击Option键，看看： ![Snip20151118_2](http://7xoguz.com1.z0.glb.clouddn.com/b2/pngSnip20151118_2.png)

从这里看，你就知道类型推导并不是多么神奇。Swift 仅是做了这个用人脑也能很容易做的事情。如果编程语言没有类型推导会很繁琐，因为每次声明变量或常量，你都要指定显式地类型。

``` 
注意：在接下来的篇节里，你将会学到更多的复杂的类型，这些类型Swift无法自动推导出。这只是非常少见的情况，在本书中的代码大部分会使用类型推导，除非我们想要强调这个类型。
```

#### Mini-exercises 迷你练习

1.声明一个元组包含2个integers，但是省略类型。点击Option键，确定类型的确是(Int, Int) 。

2.读出上面元组中第一个值，并再一次省略这个常量的类型。点击Option键，确定类型的确是Int。

## Key points 关键点

- 常量和变量用来命名数据。
- 一旦你声明一个常量，你就不能改变其数据，但是你可以改变变量的数据。
- 你总是应该给常量或者变量一个有意义的命名，避免以后难以想起，使得自己头疼。
- 你可以使用元组将一组数据转为单一数据类型。
- 类型推导可以允许你省略类型。



## Where to go from here? 然后去哪？

现在你已经了解了变量和常量，是时候关注存储的数据了！在接下来多的两个篇节，你将会两个更常见的数据类型—字符串和数字--还有如何使用它们。

## Challenges 挑战

在离开之前，还有些挑战来测试你关于常量和变量的知识。你可以尝试在playground编码来验证你的答案。

#### Challenge A: You be the compiler 挑战A：你就是编译器

下面这两块代码那个是对的？

``` 
// 1
var age = 25
age = 30

// 2
let age = 25
age = 30
```

这个代码对吗？

``` 
let tuple: (day: Int, month: Int, year: Int) = (15, 8, 2015)
let day = tuple.Day

```

#### Challenge B: Predict the outcome 挑战B：预测输出

value的类型是什么？

``` 
let tuple = (100, 1.5, 10)
let value = tuple.1
```

month的值是什么？

``` 
let tuple: (day: Int, month: Int, year: Int) = (15, 8, 2015)
let month = tuple.month

```