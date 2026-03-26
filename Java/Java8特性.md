# Java8特性知识体系

![](C:\Users\heban\Desktop\java简历and面试指北\bagu\assets\Java8特性知识体系.png)





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

一个被它注解的接口只能有一个抽象方法，有两种例外

第一是接口允许有实现的方法，这种实现的方法是用default关键字来标记的(java反射中`java.lang.reflect.Method#isDefault()`方法用来判断是否是default方法)

第二如果声明的方法和`java.lang.Object`中的某个方法一样，它可以不当做未实现的方法，不违背这个原则: 一个被它注解的接口只能有一个抽象方法, 比如: 

```java
 public interface Comparator<T> { 
     int compare(T o1, T o2); 
     boolean equals(Object obj); 
 }
 
```

如果一个类型被这个注解修饰，那么编译器会要求这个类型必须满足如下条件:

- 这个类型必须是一个interface，而不是其他的注解类型、枚举enum或者类class
- 这个类型必须满足function interface的所有要求，如你个包含两个抽象方法的接口增加这个注解，会有编译错误。

编译器会自动把满足function interface要求的接口自动识别为function interface，所以你才不需要对上面示例中的 ITest接口增加@FunctionInterface注解。



#### 内置四大函数接口

- 消费型接口: Consumer< T> void accept(T t)有参数，无返回值的抽象方法；

> 比如: map.forEach(BiConsumer<A, T>)



- 供给型接口: Supplier < T> T get() 无参有返回值的抽象方法；

> 以stream().collect(Collector<? super T, A, R> collector)为例:



- 断定型接口: Predicate<T> boolean test(T t):有参，但是返回值类型是固定的boolean

> 比如: steam().filter()中参数就是Predicate



- 函数型接口: Function<T,R> R apply(T t)有参有返回值的抽象方法；

> 比如: steam().map() 中参数就是Function<? super T, ? extends R>；reduce()中参数BinaryOperator<T> (ps: BinaryOperator<T> extends BiFunction<T,T,T>)





----------





## Lambda表达式使用时有什么特别需要注意的性质？



### lambda表达式对外部变量的访问、修改规则

#### 访问规则

lambda表达式中可以访问外部变量，但是只能是`final`关键词修饰的变量和定义后不做修改的变量





#### 修改规则

不能修改外部变量，意思就是不能在lambda内部修改定义在域外的变量。





### lambda表达式的惰性

```java
//尝试stream流中的惰性
System.out.println("---------尝试stream流中的惰性-----------");
list.stream().filter(a -> {
    System.out.println("在stream流中，没有使用终结方法，中间方法执行了");
    return true;
});
list.stream().filter(a -> {
    System.out.println("在stream流中，使用终结方法，中间方法执行了");
    return true;
}).collect(Collectors.toList());
/**
输出结果：
---------尝试stream流中的惰性-----------
在stream流中，使用终结方法，中间方法执行了
在stream流中，使用终结方法，中间方法执行了
在stream流中，使用终结方法，中间方法执行了
*/
```



