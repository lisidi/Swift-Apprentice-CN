# Chapter 8: Closures

[TOC]

前面的章节都是关于函数。但Swift还有一个对象你可以使用来让代码重用，这就是所谓的闭包。

还记得你是怎么开始处理一些清晰可见的值，如“10”和“Hello”，然后分配给他们变量名和常量名？闭包和函数是相似的。

闭包只是一个没有名字的函数。你可以将它们分配给变量，并传递。。你不需要创建一个完整格式的函数去声明他们，这样使他们用起来更方便。

## Closure basics

之所以叫作“闭包”，是因为他们可以“封锁”闭包自身作用域里的变量和常量。这意味如果闭包想要访问、存储和操纵上下文任何变量或常量，都是可以的。一个闭包里的变量和常量可以说是已被**捕获**。

你可能会问， “如果闭包是匿名函数，那么你如何使用他们？ ”使用闭包，首先必须将其分配给一个变量或常量。以这种方式，一个闭包就像任何其他类型对象。

这里是一个含有闭包的变量的声明：

``` 
var multiplyClosure: (Int, Int) -> Int
```

multiplyClosure需要两个Int值，并返回一个Int值。注意，这是完全和一个函数变量的声明一样。就像我说的，一个闭包是没有名字的函数！

你分配一个闭包给这样一个变量：

``` 
multiplyClosure = { (a: Int, b: Int) -> Int in
	return a * b 
}
```

这看起来像一个函数声明，但有一个微妙的差异。有相同的参数列表 和->符号和返回类型。但对于闭包来说，这些出现在大括号，并在返回类型后有in关键词。

闭包变量定义后，你可以像使用函数一样使用闭包，就像这样：

``` 
let result = multiplyClosure(4, 2)
```

正如你所期望的，result等于**8** 。

#### Shorthand syntax

相比于函数，闭包的设计是轻量级的。有很多方法来缩短它们的语法。首先，你可以在闭包里省略return关键字，像这样：

``` 
multiplyClosure = { (a: Int, b: Int) -> Int in
	a*b 
}
```

当闭包的最后一行包含这样的表达，Swift自动把它视为含有return。

你可以使用Swift的类型推断来缩短语法，甚至删掉返回类型：

``` 
multiplyClosure = { (a: Int, b: Int) in
	a*b 
}
```

这里唯一的区别是，你已经删除了 -> Int。请记住，你已经声明multiplyClosure闭包返回一个Int ，这样可以让Swift类型推导这返回值类型。

类型推导可以使我们语法变得更短。参数类型可以省略，像这样：

``` 
multiplyClosure = { (a, b) in
	a*b 
}
```

最后，如果你愿意，你甚至可以省略参数列表。Swift可以让你通过数字指定参数，就像这样：

``` 
multiplyClosure = {
	$0 * $1 
}
```

参数列表，返回类型和关键字都移除了，你新的闭包声明比原来的要短得多。像这样的编号参数，真的只应该用于闭包很短小时。如果闭包参数很长，你不应该用这个编号参数，而是用参数名的方式，以免参数太多让你糊涂。

现在让我们看看这个多么有用。

![Snip20151117_19](/Users/lisidi/Desktop/Swift Apprentice CN/Chapter 8: Closures/resource/Snip20151117_19.png)考虑下面代码：

``` 
func operateOnNumbers(a: Int, _ b: Int,
 operation: (Int, Int) -> Int) -> Int {
  let result = operation(a, b)
  print(result)
  return result
}
```

声明一个名为operateOnNumbers函数，前两个参数为Int类型。第三个参数被称为operation，并且它似乎是一个函数类型。 operateOnNumbers本身返回一个Int 。

然后，您可以调用operateOnNumbers函数并传递一个闭包，如下所示：

``` 
let addClosure = { (a: Int, b: Int) in
	a+b 
}
operateOnNumbers(4, 2, operation: addClosure)
```

请记住，闭包只是没有名称的函数。所以，你不应该感到惊讶，你也可以传递一个函数给operateOnNumbers的第三个参数，如下所示：

``` 
func addFunction(a: Int, b: Int) -> Int {
	return a + b
 }
operateOnNumbers(4, 2, operation: addFunction)
```

operateOnNumbers同样的方式被调用，无论该第三个参数是否是一个功能或闭包。

然而，这里的闭包语法的好处就派上用场了。你可以在

``` 
operateOnNumbers(4, 2, operation: { (a: Int, b: Int) -> Int in
return a + b })
```

这里没有必要在定义闭包时将其分配到一个局部变量或常量; 你可以简单地声明后，就将它作为参数传递给函数！

要记得，你可以通过删除了大量的样板代码来简化闭包语法。因此，可以减少以上内容变成以下内容：

``` 
operateOnNumbers(4, 2, operation: {
$0 + $1 })
```

还有另一种方式可以简化语法，但仅当闭包是传递给函数的最后一个参数。在这种情况下，你可以将闭包移动到函数外：

``` 
operateOnNumbers(4, 2) {
	$0 + $1 
}
```

这可能看起来很奇怪，但它同前面的代码片段是一样的。这就是所谓**trailing closure syntax**。

#### Closures with no return value

到现在为止，所有你见过的封锁已经采取一个或多个参数，并返回值。但就像函数一样，闭包不被要求必须做这些事情。这里告诉你如何定义一个不带参数，没有返回值的闭包：

``` 
let voidClosure: () -> Void = {
  print("Swift Apprentice is awesome!")
}
voidClosure()
```

这个闭包类型是() -> Void。空括号表示没有参数。你必须声明一个返回值类型，以便告诉Swift你声明的是一个闭包。这里void就派上用场了，void的意思是什么也不返回。

#### Capturing from the enclosing scope

最后，让我们回过头看看闭包的本质特点：它可以访问自己作用域内的变量和常量。

``` 
注意：回想一下，作用域是一个实体变量可以活动的范围。你看到的if语句引入了一个新的作用域。闭包也引入了一个新的作用域并且这个作用域继承所有实体变量作用域。
```

举个例子：

``` 
var counter = 0
let incrementCounter = {
	counter++ 
}
```

incrementCounter 相当简单：它增加counter变量。counter变量是在闭包之外定义的。闭包是能够访问变量，因为闭包与counter是在同一作用域内定义的。闭包捕获了counter变量。闭包可以更改他的里面与外面的变量。

我们调用这个闭包5次：

``` 
incrementCounter()
incrementCounter()
incrementCounter()
incrementCounter()
incrementCounter()
```

调用5次后，counter将会等于5.

事实上闭包可用来从封闭作用域内捕获变量，这是非常有用的。例如，你可以写这个函数：

``` 
func countingClosure() -> (() -> Int) {
  var counter = 0
  let incrementCounter: () -> Int = {
    return counter++
  }
  return incrementCounter
}
```

这个函数不带参数，返回一个闭包。闭包没有参数然后返回一个Int，并返回一个Int 。

每当这个函数被调用，它返回的闭包都将递增其内部的counter

。每次调用这个函数，你都会得到一个不同的counter。

举个例子：

``` 
let counter1 = countingClosure()
let counter2 = countingClosure()
counter1() // 0
counter2() // 0
counter1() // 1
counter1() // 2
counter2() // 1
```

该函数创建的两个counter是相互排斥的，独立计数。优雅！

这就是闭包！

## Key points

- **闭包**是没有名字的函数。它可以被赋值给一个变量或作为参数传递给函数。
- 闭包有**简写**语法，比函数更容易使用。
- 闭包可以**捕获**其上下文的变量和常量。

## Where to go from here?

