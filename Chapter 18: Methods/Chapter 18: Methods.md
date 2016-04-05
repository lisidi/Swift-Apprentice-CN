# Chapter 18: Methods

[TOC]

在前面的章节中,您学习了属性, 这是常出现在结构体、类和枚举中。**Methods**, 如你已经看到的, 仅仅是与某些特定类型相关联的函数。

在这一章,你需要仔细看看方法和初始化构造器。与属性一样, 在这一章你所学到的东西将适用于所有类型的方法。

## Method refresher

记得Array().removeLast() 吗？它移除数组中最后一项:

``` 
var numbers = [1, 2, 3]
numbers.removeLast()
let newArray = numbers // [1,  2]
```

![Snip20151117_26](http://7xoguz.com1.z0.glb.clouddn.com/b18/pngSnip20151117_26.png)

像removeLast( )这样的方法帮助你在命名类型中控制数据。

### Comparing methods to computed properties

通过**strong text**一个被计算的属性, 你可以运行代码从一个命名类型里面。这听起来很像一个方法, 那么有什么区别呢? 这是风格的问题,但有一些有用的想法来帮助你决定。Properties持有值,  你可以get和set, Methods执行工作。当一个方法就是返回一个值时，这种区别变得很模糊。