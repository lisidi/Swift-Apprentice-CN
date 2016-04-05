# Chapter 9: Optionals

[TOC]

到目前你处理过的所有的变量和常量都有具体的值。当你有一个字符串变量，如var name，它有一个与之关联的字符串值，如“Matt Galloway” 。这可能是一个空字符串，如“ ” ，但尽管如此，总是有一个值，你可以关联。

这就是Swift的内置安全功能之一：如果类型被告知是Int，或String，那么一定保证会有一个实际的整数值或字符串值出现。

本章将介绍optionals的内容，一个特殊的Swift类型，它可能含有一个值，也可能没有值。通过本章，你就知道为什么你需要optionals以及如何安全地使用它们。

## Introducing nil

有时，有一个空值是很有用的。想象一下这样一个场景，你需要获得一个人的身份信息。被存储人的姓名，年龄和职业。姓名和年龄都是必须有一个确切值 -- 因为每个人都有。但并非所有人都被雇佣，因此你需要让occupation值的缺失。

让我们一起来看看。

不知道optionals的情况下，下面这是你也许呈现这个人姓名，年龄和职业等信息的方式：

``` 
var name: String = "Matt Galloway"
var age: Int = 30
var occupation: String = "Software Developer & Author"
```

但如果我失业？也许我已经赢了彩票，想放弃工作（我希望！） 。这是很有用的，如果能够引用一个缺失的值。

你为什么不使用一个空字符串？嗯，你可以！让我们来讨论怎么做的，为什么optionals是一个更好的解决方案。

#### Sentinel values

一个有效的值，用来表示一个值缺失，被称为一个 sentinel value。在前面的实例中你用的空字符串就是。

![Snip20151117_20](http://7xoguz.com1.z0.glb.clouddn.com/b9/pngSnip20151117_20.png)

让我们看看另一个例子。你写一段代码去从服务器请求数据而且你使用一个变量来存储服务器返回的error代码:

``` 
var errorCode: Int = 0
```

在成功的情况下，你用0表示没有错误。这意味着 0 是 sentinel value。

就像occupation的空字符串一样，这是有效的，但它可能给程序员造成混乱。0 在未来也许是错误代码呢。无论哪种方式，你都不能完全放心相信这没有错误。

![Snip20151117_22](http://7xoguz.com1.z0.glb.clouddn.com/b9/pngSnip20151117_22.png)

在这两个例子中，如果有一种特殊的类型可以表示值缺失，那么会更好。当一个值要么存在要么缺失，这会是明确的显式的。

Nil 表示一个值的缺失。你将要看到Swift语言如何优雅的纳入这一概念。

其他一些编程语言只是使用sentinel value。比如Objective- C，有nil，但它只是一个零的同义词。它只是另一个sentinel value。

Swift 介绍了全新的类型，称为optional（可选类型），用来处理一个值为nil或非nil。这意味着，如果你正在处理一个非可选类型，那么你要它保证一定有一个确切值，而不需要担心到底有没有值。总是有一个值。同样，如果你正在使用一个optional（可选的类型）你必须处理nil的情况。

## Introducing optionals

Optionals是Swift的解决问题的办法，可以呈现一个值和值的缺失。可选的类型可以引用值或nil。

把Optionals看作为一个盒子: 它要么包含一个值，要么没有。当它不包含值时，就可以说它包含nil。盒子本身始终存在。总是在那里让你去打开或者观察里面。

 ![Snip20151117_23](http://7xoguz.com1.z0.glb.clouddn.com/b9/pngSnip20151117_23.png)

一个字符串或整数，另一方面，没有这个箱子在它周围。相反总是有一个值，例如"hello"或 42。记住，确保非可选类型都有确切值。

``` 
注意: 那些已经研究过物理的人可能会马上想到薛定谔的猫。Optionals跟它有一点像，除了它不是生与死!
```

使用下面的语法来声明一个可选的类型:

``` 
  var errorCode: Int?
```

这和标准声明的唯一区别是？在类型的后面。在这种情况下，errorCode为"optional Int"。这意味着变量本身就像一个盒子要么包含一个 Int值 要么包含一个nil。

此关系图可帮助你以可视化形式，看看发生了什么:

 ![Snip20151117_24](http://7xoguz.com1.z0.glb.clouddn.com/b9/pngSnip20151117_24.png)

可选盒子总是存在的。当你将 100 赋给变量时，你填写盒子中的值。当你分配给该变量的nil时，你清空盒子。

花几分钟去思考这一概念。

## Unwrapping optionals

可选盒子存在是非常好的，但你可能想知道如何观察和操作盒子里面的值。

看看会发生什么，当你打印一个可选值:

``` 
￼let ageInteger: Int? = 30
print(ageInteger)
```

这将打印以下结果:

``` 
Optional(30)
```

这不是你真正想要的 -- 但是仔细想想，这却很有意义。你的代码已经打印出这个盒子。结果是：ageInteger 是可选值类型，它包含的值为 30。

若要看看这个值类型和非可选的类型相比有什么不同，让我们看看像用一个普通整型的方式去使用 ageInteger：

``` 
print(ageInteger + 1)
```

触发一个错误:

``` 
error: value of optional type 'Int?' not unwrapped; did you mean to use
'!' or '?'?
```

这不能运行，因为你想要给盒子加一个整数 — 不是给盒子里的值相加，而是盒子本身。这根本没有道理!

#### Force unwrapping

错误消息说明了解决方案: 它告诉你，可选类型是没有打开的。你需要打开盒子，拿到值。就像圣诞节!

让我们看看这是如何工作。请考虑下面的声明:

``` 
var authorName: String? = "Matt Galloway"
```

有两种不同的方法，你可以用来打开这个可选值。第一种被称强制解析，你可以这么用:

``` 
￼var unwrappedAuthorName = authorName!
print("Author is \(unwrappedAuthorName)")
```

在变量名后面的！告诉编译器你想看盒子里面，并拿出值。下面是结果:

``` 
Author is Matt Galloway
```

太好了!这是你期望的。

“force"和 ! 将会向你转达一种威胁感，这是值得注意的。你应该谨慎使用强制解析。若要知道为什么，去考虑当可选值不包含一个确切值时，会发生什么:

``` 
authorName = nil
var unwrappedAuthorName = authorName!
print("Author is \(unwrappedAuthorName)")
```

此代码产生以下的运行时错误:

``` 
fatal error: unexpectedly found nil while unwrapping an Optional value
```

因为当你尝试打开它时，该变量并没有包含值，所以发生错误。更糟糕的是你在运行时获取此错误而不是在代码的编译阶段 — 这意味着只有当你碰巧执行这部分代码，你才会发现这个错误。更糟糕的是，如果这个代码在一个app里执行，运行时错误会导致应用程序崩溃!

那怎么安全的使用呢？

要在这里停止运行时错误，你可以通过检查判断却解开可选值，像这样的代码：

``` 
if authorName != nil {
  var unwrappedAuthorName = authorName!
  print("Author is \(unwrappedAuthorName)")
} else {
  print("No author.")
}
```

if语句检查可选值是否包含nil。如果不包含，这意味着它包含一个确切值，就可以解开。

该代码现在是安全的，但它仍然不是完美的。如果靠这种技术去解开一个可选值，你必须每次记住去检查nil。这将开始变得乏味，有一天你会忘记，运行时错误可能还会发生。

#### If let binding

幸运的是，Swift包含一个功能被称为**if let binding**，它可以让你安全地访问一个可选值内部的值。你可以使用它，如下所示：

``` 
if let unwrappedAuthorName: String = authorName {
  print("Author is \(unwrappedAuthorName)")
} else {
  print("No author.")
}
```

你会马上注意到这里没有 ！ 还有 unwrappedAuthorName 的类型是一个普通的字符串类型，不是一个可选的字符串类型。

``` 
注意: 通常你不用指定未解开变量的类型在这个if let语句中，但它在此处显示是为了看的清晰。
```

这种特殊的语法摆脱了可选类型。如果可选类型变量包含一个值，那么代码会执行  if 语句，在if 语句中你自动打开 unwrappedAuthorName 变量，因为你知道这么做是安全的。

如果可选类型变量不包含值，则执行else部分代码。在这种情况下，unwrappedAuthorName 变量甚至根本不存在。

你可以看到if let binging比强制解析更安全，你应该尽可能选择f let binging。

你甚至可以同时打开多个值，就像这样:

``` 
let authorName: String? = "Matt Galloway"
let authorAge: Int? = 30
if let name: String = authorName,
       age: Int = authorAge {
  print("The author is \(name) who is \(age) years old.")
} else {
  print("No author or no age.")
}
```

此代码打开两个值。当可选包含值时，它只会执行 if 部分。

现在你知道如何安全地观察和提取可选类型变量里的值 了吧。

## Nil coalescing

最后还有一个相当方便的方法去打开一个可选值。当你想要从一个可选值中取出一个值，并且这个可选值不管是nil还是其他什么情况，  此时你使用这个方法，你都将会用一个默认值。这就是所谓**nil coalescing**。

看看怎么做的：

``` 
￼var optionalInt: Int? = 10
var result: Int = optionalInt ?? 0
```

nil coalescing发生在第二行，还带有??。该行表示result将等于optionalInt内部的值，或者等于0（如果optionalInt包含nil）。

所以在这个例子中，result包含整型值10。

以上的代码等效于以下：

``` 
var optionalInt: Int? = 10
var result: Int
if let unwrapped = optionalInt {
  result = unwrapped
} else {
result = 0 
}
```

将 optionalInt 设置为nil，就像这样:

``` 
￼optionalInt = nil
var result: Int = optionalInt ?? 0
```

现在result等于0。

## Key points

- Nil表示没有值。
- 非可选变量和常量必须始终有一个非空值。
- 可选变量和常量就像一个盒子可以包含一个值或者空的 (nil)
- 想要处理可选变量内部值，你必须首先打开可选变量。
- 最安全的方法来打开可选变量是通过使用if let binding或nil coalescing。避免强制解析，因为它可能会产生运行时错误。