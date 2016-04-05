# Chapter 17: Properties

[TOC]

到目前为止,这本书介绍了三种“命名类型”: 结构体、类和枚举。使用它们，来组织属性和公共重用的行为，让你成为一个更高效的程序员。

在下面的示例中,Car结构体有两个属性, 这两个常量存储字符串值：

``` 
struct Car {
  let make: String
  let color: String
}
```

像这样的属性,和那些其他命名类型, 被称为属性。汽车的两个属性都存储属性,Car的两个属性都存储着这意味着他们为汽车的每个实例存储实际的字符串值。类和结构可以存储属性。

某些属性计算值，而不是将它们存储起来; 这意味着没有实际的内存空间分配给他们，但是当每次访问他们的时候，他们将被被计算。自然地，这些被称为**computed properties**。类和结构体可以有computed properties，枚举也可以。

在本章中，你将了解这两种属性。你还将了解其他一些巧妙的技巧来处理属性，比如，怎么在“一个属性的值延迟一个存储属性的初始化”的情况下 检测变化。

## Stored properties

正如你从上面例子猜到的，你已经熟悉了stored properties的许多特点。回顾一下，想象你正在构建一个地址簿。你需要的基本单元是Contact：

``` 
struct Contact {
  var fullName: String
  var emailAddress: String
}
```

你可以使用这个结构体一遍又一遍，帮你建立联系人的数组，每个都有不同的值。要存储的成员变量是一个人的全名和电子邮件地址。

 ![Snip20151117_25](http://7xoguz.com1.z0.glb.clouddn.com/b17/pngSnip20151117_25.png)

这些是Contact结构体的属性。你为每一个联系人提供数据类型，但并不分配一个默认值，因为你想在初始化的时候分配值。毕竟，对于Contact的每一个实例，他们的值都是不同的。

要记住的是，Swift根据你在结构体中定义的属性，自动创建一个初始化构造器：

``` 
￼var person = Contact(fullName: "Grace Murray",
 emailAddress: "grace@navy.mil")
```

你可以使用点语法访问私有属性：

``` 
￼let name = person.fullName // Grace Murray
let email = person.emailAddress // grace@navy.mil
```

只要属性被定义为变量，你就可以给属性分配值。当格雷斯结婚后，她改变了她的姓氏：

``` 
￼person.fullName = "Grace Hopper"
let grace = person.fullName // Grace Hopper
```

如果你想让这样的值不能更改，你可以改为用常数定义属性:

``` 
struct Contact {
  var fullName: String
  let emailAddress: String
}
// Error: cannot assign a constant
person.emailAddress = "grace@gmail.com"
```

一旦你已经初始化一个这种结构体类型的实例，你就不能更改emailAddress。

#### Default values

如果你可以做一个合理的假设，关于什么值应该初始化类型时，你可以给该属性一个默认值。

这是没有道理的去为一个联系人创建默认名称或电子邮件地址，但想一下如果有一个新的属性type表示联系人是何种种类，像这样:

``` 
enum Type {
  case Work, Family, Friend
}
struct Contact {
  var fullName: String
  let emailAddress: String
  var type: Type = .Friend
}
```

通过在contact的定义中包括转让，你给它一个默认值。任何从这个结构体实例化出的contact都将会成为朋友，除非您将该值更改为.work或 .Family。

缺点是自动初始化构造器没有复制一个默认值，所以你仍然需要为每个属性提供一个值，除非你创建你自定义初始化构造器。在下一章中你会了解更多有关创建初始化构造器。

## Computed properties