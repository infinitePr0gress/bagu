# Java8特性知识体系

![](C:\Users\heban\Desktop\java简历and面试指北\八股\assets\Java8特性知识体系.png)





# 函数编程（Lambda表达式）



## 什么是Lambda表达式？作用是什么？

Lambda表达式是一种匿名函数，作用是为了实现函数式编程。lambda表达式在Java中又叫做闭包、匿名函数。



## Lambda的语法结构是什么样的？

语法结构是：`(参数) -> {核心执行代码};`这是正常的写法

如果核心代码处不修改lambda表达式提供的参数。那么可以使用方法引用。

``` java
list.forEach(n -> System.out.println(n)); 
list.forEach(System.out::println);  // 使用方法引用
```

如果修改lambda表达式提供的参数，那么就不能使用方法引用

``` java
list.forEach((String s) -> System.out.println("*" + s + "*"));//只能这么写
```



## 什么时候可以使用Lambda表达式？

当且仅当目标类型是**函数式接口**时才可以使用。

---- > 那什么是函数式接口呢？

> **函数式接口指的是 ： 只包含一个抽象方法的接口**，并且都会带有`@FunctionalInterface`注解



## Lambda表达式使用时有什么特别需要注意的？

- lambda表达式中可以访问外部变量，但是不能修改外部变量，意思就是不能在lambda内部修改定义在域外的变量。
- 



