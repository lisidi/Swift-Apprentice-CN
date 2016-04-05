# Chapter 7: Functions

[TOC]

函数是很多编程语言的核心。简单地说，一个函数就是你定义的代码块， 通过这个代码块去完成某些特定的任务。然后，无论何时你的app需要执行某个特定任务，你都可以运行这个函数，而不必到处复制和粘贴相同的代码。

在本章中，您将学习如何编写自己的函数，并亲眼目睹Swift如何使它们易于使用。

## Function basics

假设你有一个应用程序，经常需要打印你的名字。您可以编写一个函数来做到这一点：

``` 
func printMyName() {
  print("My name is Matt Galloway.")
}
```

上面的代码被称为函数声明。您可以通过使用func关键字去定义一个函数。接着是函数的名称，后面接个括号。您将了解更多有关需要对这些括号在下一节。

括号后的是大括号，其次是在函数里运行的代码，随后右大括号。函数定义好后，你可以这样用它：

``` 
printMyName()
```

这样就会打印出以下片段：

``` 
My name is Matt Galloway.
```

如果您怀疑自己已经使用过一个函数在以前的章节中，那么你想的是对的！print，将你编写的代码打印到控制台，这的确是一个函数。这让我们很好地进入下一环节，你将学习如何将数据传递到函数和再从函数中拿回数据。

 ![Snip20151117_17](http://7xoguz.com1.z0.glb.clouddn.com/b7/pngSnip20151117_17.png)

#### Function parameters

在上一个例子中，函数只是打印出一条消息。这很棒，但有时你希望你的函数有参数，可以通过传入参数的不同去执行不同的任务。作为一个例子，看看下面这个函数：

作为一个例子，看看下面的函数：

``` 
func printMultipleOfFive(multiplier: Int) {
  print("\(multiplier) * 5 = \(multiplier * 5)")
}
```

``` 
printMultipleOfFive(10)
```

在这里，你可以看到函数名后面的括号内的一个参数的定义。这就是所谓的乘数是int类型。在任何函数中，括号里面的是所谓的参数列表。

该函数将打印出传入参数值的5倍。在该例中，将调用函数并传入10，所以函数打印以下内容：

``` 
10 * 5 = 50
```

你可以借此更进一步，让函数更通用化。有两个参数，函数可以打印出任何两个值的倍数。你可以做到这一点，如下所示：

``` 
func printMultipleOf(multiplier: Int, andValue: Int) {
  print("\(multiplier) * \(andValue) = \(multiplier * andValue)")
}
```

``` 
printMultipleOf(4, andValue: 2)
```

现在有括号内两个参数的函数名后：一个叫乘数，另一个叫andValue 。这两个都是int类型。

这个时候，当你调用该函数的同时你要传递两个值。请注意，第二个参数有一个参数名在前。这个语法就是Swift风格， 这种风格让你写出的代码看起来像一句话。在上面一行代码，你将会这样读出来：

``` 
Print multiple of 4 and value 2
```

你可以通过给参数一个不同的外部变量名使代码看起来更加清晰。例如，您可以更改andValue参数的外部名称：

``` 
func printMultipleOf(multiplier: Int, and andValue: Int) {
  print("\(multiplier) * \(andValue) = \(multiplier * andValue)")
}
```

``` 
printMultipleOf(4, and: 2)
```

你可以通过把名字写在参数名前，去指定一个不同的外部变量名。在这个例子中， andValue仍是参数名称，但在函数调用的时候显示的标签是and。你可以这样上面这行代码：

``` 
Print multiple of 4 and 2
```

如果你想没有外部变量名的话，那么你可以使用下划线_ ，因为你已经看到了前面的章节：

``` 
func printMultipleOf(multiplier: Int, _ andValue: Int) {
  print("\(multiplier) * \(andValue) = \(multiplier * andValue)")
}
```

``` 
printMultipleOf(4, 2)
```

在本例中，第二个参数没有外部变量名，就像第一个参数一样。但使用下划线明智。但一个复杂的函数，在没有外部变量名时去持有多个参数就会变得更加复杂和笨拙。试想一下，如果一个函数用了五个参数！

 ![Snip20151117_18](http://7xoguz.com1.z0.glb.clouddn.com/b7/pngSnip20151117_18.png)

你也可以给参数默认值：

``` 
func printMultipleOf(multiplier: Int, and andValue: Int = 1) {
  print("\(multiplier) * \(andValue) = \(multiplier * andValue)")
}
```

``` 
printMultipleOf(4)
```

不同的是 在第二个参数后的“ = 1 ”，这意味着如果没有给第二个参数传值，则二个参数默认为1。

4 * 1 = 4

有一个默认值会非常有用，当你期望参数通常是一个值，并且当你调用函数时，它将简化你的代码。

#### Return values

所有你目前所见过的函数都是执行一个简单的任务，即打印函数。函数可以返回一个值。函数的调用方可以将返回值赋给一个变量或常量。

这意味着你可以使用函数来操作数据。你可以简单的通过参数传递数据，对参数进行操作，然后返回参数。这里是你如何定义一个函数，返回一个值:

``` 
func multiply(number: Int, by byValue: Int) -> Int {
  return number * byValue
}
let result = multiply(4, by: 2)
```

若要声明一个带有返回值的函数，你添加-> 还有返回值的类型。这个例子返回了一个Int值。在函数内部使用 return 关键字返回值。在此示例中，您返回两个参数的乘积。

它也可能使用元组返回多个值:

``` 
func multiplyAndDivide(number: Int, by byValue: Int) -> (multiply: Int,
divide: Int) {
  return (number * byValue, number / byValue)
}
let result = multiplyAndDivide(4, by: 2)
let multiply = result.multiply
let divide = result.divide
```

此函数返回两个参数的乘积和商。通过返回一个元组实现。通过元组返回多个值的特性使得我们很高兴使用Swift。它是一个非常有用的功能，你很快就会看到。

#### Advanced parameter handling

默认情况下，传递给函数的参数是常量，这意味着他们不能修改。为了说明这一点，请考虑下面的代码:

``` 
func incrementAndPrint(value: Int) {
  value++
  print(value)
}
```

这会导致错误:

``` 
Cannot pass immutable value to mutating operator: 'value' is a 'let' Constant

```

参数值是用let声明一个常量。因此，当函数将尝试递增，编译器会引发错误。

您可以更改此行为，通过让该参数作为变量：

``` 
func incrementAndPrint(var value: Int) {
  value++
  print(value)
}
```

现在，value是一个变量，该函数可以递增它。

此函数说明了另一个有趣点，关于函数参数。看看会发生什么，当你调用上述函数:

``` 
var value = 5
incrementAndPrint(value)
print(value)
```

将打印出：

``` 
6
5
```

这可能是不直观的。你初始化一个value变量并传递value给函数，使该变量递增到6。但是，当最后一行打印value，但它仍然等于5，这是为什么？

这是因为Swift在传递给函数之前，拷贝了值，称为值传递。

注：值传递和copy是所有类型的标准行为。你会看到另一种方式去传递一些东西给函数在第14章， “类” 。

通常你想要这种行为。理想情况下，函数不会改变其参数。如果改变了，那么你也不能肯定参数的值，你可能会做出不正确的假设在你的代码，从而导致错误的数据。

有时候，你想让一个函数直接改变一个参数， 引用传递。如下所示：

``` 
func incrementAndPrintInOut(inout value: Int) {
  value++
  print(value)
}
```

现在，你需要做点小文章 对于函数调用：

``` 
var value = 5
incrementAndPrintInOut(&value)
print(value)
参数前添加一个
```

＆符号，帮你记住参数是使用引用传递。现在该函数可以更改值。

本示例将打印以下内容:

``` 
6
6
```

这一次，该函数成功递增value的值，这个value的值持有的是函数执行完毕修改后的数据。这是因为如果参数函数去，然后回来出来见面，因为这个 inout 关键字。

#### Examples from the standard library

Swift标准库包含许多为你准备好的的函数。

你已经见过一个在整本书中都在调用的函数: 打印。它采用单个字符串参数，并将参数打印到控制台。

有几个数学函数需要记住因为他们 经常被使用。

第一个是max，其中采用两个值并返回最大值:

``` 
let result = max(10, 20)
```

在此示例中，结果等于 **20**。

同样，min取出两个值，并返回最小值:

``` 
let result = min(10, 20)
```

在这里，结果等于 **10**。

最后，abs 取一个值，并返回绝对值，即原始值的非负版本。例如，-10 的绝对值是 10，而 10 的绝对值是 10。这里是Swift的函数:

``` 
let result = abs(-10)
```

这一次，结果等于 **10**。

当你继续使用 Swift，你会从这个标准库遇到许多其他的功能。你不能把它们都记住，但重要的是你需要知道是许多预定义的功能是存在的。如果你想做什么，然后进行搜索。没有任何意义重复造轮子。

## Functions as variables

这可能是一个惊喜，就是 函数在Swift中只是其中的一种数据类型。你可以将它们分配给变量和常量，就像你可以把一个Int值或者字符串赋值给一个变量或者常量。

若要看这是怎么实现的，请考虑下面的函数:

``` 
func add(a: Int, _ b: Int) -> Int {
return a + b 
}
```

这两个参数并返回它们的总和。您可以将此函数分配给一个变量，如下所示:

``` 
var function: (Int, Int) -> Int = add
```

在这里，变量的名称是函数，它的类型是 (Int，Int) -> Int. 你将把函数分配给此变量。类型定义是重要的虽然。你定义这个变量同样要写上像原来一样写上参数和返回值。在这里，函数变量是一种函数类型，可以取两个 Int 参数并返回一个整型数。

现在你可以像似以前调用函数的方式去使用函数变量:

``` 
let result = function(4, 2)
```

在此示例中，结果等于 6。现在考虑下面的代码:

``` 
func subtract(a: Int, _ b: Int) -> Int {
	return a - b 
}
```

在这里，你声明另一个函数有两个 Int 参数并返回一个整数值。你可以将function函数变量赋值给subtract函数变量，因为参数列表和返回类型的subtract变量与function变量的类型兼容。

``` 
￼function = subtract
let result = function(4, 2)
```

这一次，结果等于 2。

事实上，你可以分配一个函数给一个变量，这是很用用的，因为这意味着你可以将函数传递给其他函数。这里是一个这样的例子在行动:

``` 
func printResult(function: (Int, Int) -> Int, _ a: Int, _ b: Int) {
  let result = function(a, b)
  print(result)
}
printResult(add, 4, 2)
```

printResult 用了三个参数: 

1. function是需要两个 Int 参数并返回一个整型数的函数类型，声明像这样: (Int，Int) -> Int
2. a没有外部的名称并且是类型Int。
3. b没有外部名称并且是类型Int。 printResult 传递function函数，传递两个 Int 参数。然后它将结果打印到控制台:

``` 
6
```

能够将函数传递给其他函数，这是非常有用的。它也可帮助你编写可重用的代码。你不仅可以传递数据，也可以将函数作为参数传递，这使得你处理代码更加灵活。

## Key points

- 你可以使用一个函数定义任务，这个任务你可以执行很多次，但只需要写一次代码。
- 函数可以采取零个或多个参数，可以有或无返回值。
- 函数的第一个参数在函数调用时都没有标签显示。所有后面的参数都标有他们的名字。
- 你可以给一个参数名加一个外部变量名去改变调用时的标签，或者你可以使用下划线来表示没有标签。
- 可以将函数赋给变量并将它们传递给其他函数。