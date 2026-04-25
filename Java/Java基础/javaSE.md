



https://xiaolincoding.com/interview/collections.html



#  一 、对象与类

什么是对象？

对比面向过程，是两种不同的处理问题的角度

面向过程更注重事情的每一个步骤以及顺序，面向对象更注重事情有哪些参与者（对象）、以及各自需要做什么

举一个例子：洗衣机洗衣服

面向过程会将任务拆解成一系列的步骤（函数），

1.打开洗衣机---->2.放衣服------>3.放洗衣粉-------->4.清洗--------->5.烘干

面向对象会拆出人和洗衣机两个对象：

人：打开洗衣机，放衣服，放洗衣粉

洗衣机：清洗，烘干



从以上例子可以看出，面向过程比较直接高效，而面向过程更易于复用、拓展和维护





## 创建对象的方式

- **使用 new 关键字**（最基础、最常用）
- **使用 `Class.newInstance` ()**（反射，已废弃）
- **使用 `Constructor.newInstance ()`**（反射，推荐）
- **使用 clone () 方法**
- **使用反序列化**
- **使用 工厂方法 / 静态工厂**（设计模式）

扩展一下，这六种创建对象方式中只有`clone()`和使用反序列化是不调用构造方法的

> 使用构造方法的都有一个特性，从零开始创建，分配内存----初始化默认值---执行构造方法；会按照我们编写的代码逻辑执行，**有整个的构造过程**
>
>
> 
> 但是，反序列化和clone()方法是不同的，它俩不是按照编写代码逻辑执行
> 比如clone(),在`jvm`堆中分配了一个内存地址后，它是直接复制原对象中的属性值，而不是先初始化默认值，再设置为原对象中属性的值。**没有完整的构造过程**





==**下面是一些零零碎碎的笔记**==





## 继承

> 构造方法中的this使用：
>
> - **调用当前类的其他构造方法**
> - **引用当前对象的属性和方法**
> - **区分属性和参数**



1. 



### this关键字和super关键字



#### this

1. **引用当前对象**：
   - `this` 关键字用于在类的方法或构造方法中引用当前对象本身。
   - 它可以用来访问当前对象的成员变量和调用当前对象的其他方法。
2. **区分成员变量和局部变量**：
   - 当方法的参数名与类的成员变量名相同时，`this` 可以用来明确指出成员变量。
3. **调用当前对象的其他方法**：
   - 在一个方法中，可以使用 `this` 来调用同一个对象的其他方法。
4. **构造方法链**：
   - 在构造方法中，`this` 可以用来调用同一个类的其他构造方法。
5. **返回当前对象的引用**：
   - 方法可以返回 `this`，从而允许方法链式调用。





#### super



子类调用父类的构造方法，并且在父类构造方法中传参  super(String name)这样，不会使得子类的name属性被赋值，只会让父类的name属性被赋值 

1. **引用父类对象**：
   - `super` 关键字用于在子类的方法或构造方法中引用父类对象。
   - 它可以用来访问父类的成员变量和调用父类的方法。
2. **调用父类的构造方法**：
   - 在子类的构造方法中，`super` 可以用来调用父类的构造方法。
   - 如果子类的构造方法中没有显式调用 `super`，则默认调用父类的无参构造方法。
3. **解决继承中的名称冲突**：
   - 当子类和父类有同名的成员变量或方法时，`super` 可以用来明确指出父类的成员。
4. **访问父类的私有成员**：
   - 通过 `super`，子类可以访问父类的私有成员变量和方法，只要这些成员在子类中被子类的方法或构造方法访问。









### final关键字

final是一个关键字，可以用于修饰类，成员变量，成员方法。**final是写在返回类型前面的**

#### **特点**：

1. 它修饰的类不能被继承。
2. 它修饰的成员变量是一个常量。
3. 它修饰的成员方法是不能被子类重写的。

final修饰的常量定义一般都有书写规范,被final修饰的常量名称,所有字母都**大写**。

final修饰成员变量,必须初始化,初始化有两种

- 显示初始化；
- 构造方法初始化。
  但是不能两个一起初始化

#### **final和private的区别**：

1. final修饰的类可以访问；
   private不可以修饰外部类，但可以修饰内部类（其实把外部类私有化是没有意义的）。
2. final修饰的方法不可以被子类重写；
   private修饰的方法表面上看是可以被子类重写的，其实不可以，子类是看不到父类的私有方法的。
3. final修饰的变量只能在显示初始化或者构造函数初始化的时候赋值一次，以后不允许更改；
   private修饰的变量，也不允许直接被子类或一个包中的其它类访问或修改，但是他可以通过set和get方法对其改值和取值。





### 方法重写和重载



#### 方法重写

##### 概念：

重写是[子类](https://so.csdn.net/so/search?q=子类&spm=1001.2101.3001.7020)对父类的允许访问的方法的实现过程进行重新编写, 返回值和形参都不能改变。即外壳不变，核心重写！

对方法内容进行修改。





#### 方法重载

##### 概念：

重载(overloading) 是在一个类里面，方法名字相同，而参数不同。返回类型可以相同也可以不同。

##### 注意

每个重载的方法（或者构造函数）都必须有一个独一无二的参数类型列表。

最常用的地方就是构造器的重载。

##### 重载规则：

被重载的方法必须改变参数列表(参数个数或类型或顺序不一样)；
被重载的方法可以改变返回类型；
被重载的方法可以改变访问修饰符；
被重载的方法可以声明新的或更广的检查异常；
方法能够在同一个类中或者在一个子类中被重载。
无法以返回值类型作为重载函数的区分标准。



#### 重载和重写的区别

| 区别点   | 重载方法 | 重写方法                                       |
| -------- | -------- | ---------------------------------------------- |
| 参数列表 | 必须修改 | 一定不能修改                                   |
| 返回类型 | 可以修改 | 一定不能修改                                   |
| 异常     | 可以修改 | 可以减少或删除，一定不能抛出新的或者更广的异常 |
| 访问     | 可以修改 | 一定不能做出更严格的限制（可以降低限制）       |





## `object`类

###  == 与 equals 有什么区别？

1. 对于**字符串**变量来说，使用`==`和`equals`比较字符串时，其比较方法不同。`==`比较两个变量本身的值，即两个对象在内存中的首地址，`equals`比较字符串包含内容是否相同。因为在`String`类中重写了`equals`方法

``` java
//String类中的equals()方法:
public boolean equals(Object anObject) {
    if (this == anObject) {
        return true;
    }
    if (anObject instanceof String) {
        String aString = (String)anObject;
        if (coder() == aString.coder()) {
            return isLatin1() ? StringLatin1.equals(value, aString.value)
                              : StringUTF16.equals(value, aString.value);
        }
    }
    return false;
}
```

​	2.对于非字符串变量来说，如果没有对equals()进行重写的话，"==" 和 "equals"方法的作用是相同的，都是用来比较对象在堆内存中的首地址，即用来比较两个引用变量是否指向同一个对象。

``` java
//Oject类中的equals()方法：
public boolean equals(Object obj) {
    return (this == obj);
}
//没有重写equals方法的前提下，两种比较方法是一样的。
```

- ==：比较的是两个字符串内存地址（堆内存）的数值是否相等，属于数值比较；
- equals()：比较的是两个字符串的内容，属于内容比较。



### `hashcode`和`equals`方法有什么关系？

在 Java 中，对于重写 `equals` 方法的类，通常也需要重写 `hashCode` 方法，并且需要遵循以下规定：

- 一致性：如果两个对象使用`equals()`方法比较结果为true，那么他们的`hashCode`值必须相同，也就是说，如果`obj1.equals(obj2)`返回 true ，那么`obj1.hashCode()`必须等于`obj2.hashCode()`。
- 非一致性：如果两个对象的 `hashCode` 值相同，它们使用 `equals` 方法比较的结果不一定为 true。即 `obj1.hashCode() == obj2.hashCode()` 时，`obj1.equals(obj2)` 可能为 false，这种情况称为哈希冲突。

`hashCode` 和 `equals` 方法是紧密相关的，重写 `equals` 方法时必须重写 `hashCode` 方法，以保证在使用哈希表等数据结构时，对象的相等性判断和存储查找操作能够正常工作。而重写 `hashCode` 方法时，需要确保相等的对象具有相同的哈希码，但相同哈希码的对象不一定相等。

重写equals方法之后没有重写`hashCode`方法，就会导致



## static



### 静态变量

被`static`修饰的成员变量，叫做静态变量，静态变量是随着类的加载而加载的，优先于对象的出现

特点：

- 被该类所有对象共享
- 不属于对象，属于类
- 随着类的加载而加载，优先于对象存在

调用方法：

- 类名调用(推荐)
- 对象名调用



在堆内存中有一块区域，叫做静态存储位置（静态区），会把静态变量（静态方法还是在方法区中）单独存储在这里面



### 静态方法

被`static`修饰的成员方法，叫做静态方法

特点：

- 多用在测试类和工具类中
- `javabean`类中很少会使用到

调用方法：

- 类名调用
- 对象名调用



### `static`注意事项

- 静态方法只能访问静态变量和静态方法
- 非静态方法可以访问静态变量或者静态方法，也可以访问非静态的成员变量和非静态的成员方法
- 静态方法中是没有`this`关键字的



静态方法找变量是在静态区中找的



#### 总结

静态方法中，只能访问静态

非静态方法中可以访问所有

静态方法中没有`this`关键字





## 内部类

#### 静态内部类

- 静态内部类是定义在另一个类（外部类）内部的类，但它可以独立于外部类的实例存在。
- 静态内部类可以访问外部类的静态成员，但不能直接访问非静态成员，除非通过外部类的实例





#### 匿名内部类

简单来说就是隐藏了名字的内部类，可以写在成员位置，也可以写在局部位置。

匿名内部类的格式：

``` java
new 类名或者接口名(){
    重写方法;
};

/*
格式细节：
继承或者实现---类名或者接口名
方法重写---重写方法
创建对象---new

整体就是一个类的子类对象或者接口的实现对象
*/
```



##### 知识理解

``` java
@FunctionalInterface
public interface Function<T, R> {
    /**
     * Applies this function to the given argument.
     *
     * @param t the function argument
     * @return the function result
     */
    R apply(T t);
}

//下面是一个接口
public interface animal(){
    public void eat(Function<R,T> function);
}

public class Test{
    @Test
    public void test(){
        animal animal = new animal(); 
        animal.eat(new Function(){
          	@Override
            R apply(T t){}
        };)
    }
}


```



##### 使用场景：

当方法的参数是接口或者类时，以接口为例子，可以床底这个接口的实现类对象,如果实现类只使用一次，就可以用匿名内部类简化代码











## 权限修饰符

- 权限修饰符：是用来控制一个成员能够被访问的范围的
- 可以修饰成员变量、方法、构造方法、内部类

有四种权限修饰符（`private` < 空着不写 < protected < public）



## 代码块

### 局部代码块

提前结束变量的生命周期（已淘汰）

### 构造代码块

构造代码块就是写在成员位置的代码块

可以用来把构造方法中重复出现的代码提出来

执行时机：我们在创建本类对象的时候会先执行构造代码块再执行构造方法

```java
public class Student{
	private String name;
	private int age;
	
	public Student(){
		System.out.println("开始创建对象了");
	}
	
	public Student (String name,int age){
		System.out.println("开始创建对象了");
		this.name = name;
		this.age = age;	
	}
}

//可以改写为这种构造代码块

public class Student{
	private String name;
	private int age;
    {
    	System.out.println("开始创建对象了");
    }
    
    
	public Student(){
	}
	
	public Student (String name,int age){
		this.name = name;
		this.age = age;	
	}
}

```





### 静态代码块

格式：`static`{....}

特点：需要通过`static`关键字修饰，==随着类的加载而加载==，并且自动触发，只执行一次

使用场景：在类的加载的时候，做一些数据初始化的时候使用



> 静态代码块中不能声明抛出异常，如果要抛出异常的话只能使用try{...} catch{...}





## 字符串

[字符串原理,阿玮版](https://www.bilibili.com/video/BV17F411T7Ao?t=13.4&p=107)



#### `String`类

1. **不可变性**：
   - `String`对象是不可变的。这意味着一旦创建了一个`String`对象，它的值就不能被改变。每次对`String`对象进行修改操作（如拼接、替换等），实际上都会创建一个新的`String`对象。
2. **线程安全**：
   - 由于`String`对象的不可变性，**它们是线程安全的**。因此，`String`对象可以在多线程环境中安全使用，不需要额外的同步措施。
3. **性能**：
   - 对于频繁修改字符串的场景，使用`String`可能会导致性能问题，因为每次修改都会创建新的对象。
4. **内存使用**：
   - `String`对象在Java的字符串常量池中存储，如果字符串是字面量或者通过`String`的字面量语法创建的，那么相同的字符串字面量会指向同一个对象。
5. **使用场景**：
   - 适用于不需要频繁修改的字符串场景，如常量字符串、数据库查询语句等。



#### `StringBuffer`

1. 可变性：
   - `StringBuffer`对象是可变的。这意味着你可以修改`StringBuffer`对象的内容，而不需要创建新的对象。
2. 线程安全：
   - `StringBuffer`是线程安全的，因为它在内部对所有公共方法都进行了同步。这使得`StringBuffer`可以在多线程环境中安全使用。
3. 性能：
   - 对于需要频繁修改字符串的场景，`StringBuffer`通常比`String`更高效，因为它不需要频繁创建新的对象。
4. 内存使用：
   - `StringBuffer`对象不存储在字符串常量池中，每次修改都会直接在对象本身上进行。
5. 使用场景：
   - 适用于需要频繁修改字符串的场景，如动态构建字符串、多线程环境中的字符串操作等。



#### `StringBuilder`

- 从Java 5开始，引入了`StringBuilder`类，它是`StringBuffer`的非同步版本。`StringBuilder`在单线程环境中提供了更好的性能，因为它不需要进行同步操作。

![](C:\Users\heban\Desktop\java简历and面试指北\bagu\assets\String、StringBuilder、StringBuffer区分.png)



## 包装类

包装类：基本数据类型对应的对象

JDK5以前的方法只需要了解即可

JDK5的时候包装类提出了自动装箱和自动拆箱



**一般不会使用包装类进行运算，因为包装类可以是null**



### Integer成员方法

| 方法名                                       | 说明                                |
| -------------------------------------------- | ----------------------------------- |
| `public static String toBinaryString(int i)` | 得到二进制                          |
| `pubic static String toOctalString(int i)`   | 得到八进制                          |
| `public static String toHexString(int i)`    | 得到十六进制                        |
| `public static int parseInt(String s)`       | 将字符串类型的整数转成int类型的整数 |

















# 二、常用API



## 工具类

### Collectors

`Collections` 工具类位于 Java 的 `java.util` 包中

> ### `返回List集合: toList()`
>
> 用于将元素累积到`List`集合中。它将创建一个新`List`集合（不会更改当前集合）。
>
> ```java
> List<Integer> integers = Arrays.asList(1,2,3,4,5,6,6);
> integers.stream().map(x -> x*x).collect(Collectors.toList());
> // output: [1,4,9,16,25,36,36]
> ```





## `BigInteger`

| 构造方法                                     | 说明                                                         |
| -------------------------------------------- | ------------------------------------------------------------ |
| `public BigInteger(int num, Randomrnd)`      | 获取随机大的整数，范围 ： [0 ~ 2的num - 1次方]               |
| `public BigInteger(String val)`              | 获取指定大的整数                                             |
| `public BigInteger(String val, int radix)`   | 获取指定进制的大整数                                         |
| `public static BigInteger valueOf(long val)` | 静态方法获取`BigInteger`的对象，内部有优化，表示范围较小，只能在long的范围内<br />在内部对常用的数字（ -16 ~ 16 ）进行了优化，提前创建好对象，多次获取不会创建新的 |

==注意== ： 对象一旦创建，内部记录的值是不能发生改变的



## 正则表达式



### 爬虫

```java
//Pattern:表示正则表达式
//Matcher:文本匹配器，作用：按照正则表达式的规则去读取字符串，从头开始读取
//					在大串中去找符合匹配规则的子串

Pattern p = Pattern.compile("regex");//静态方法获取正则表达式的对象
//获取文本匹配器的对象
//m : 我呢本匹配器的对象
//str : 大串（文本）
//p : 规则
//m要在str中找符合p规则的小串
Matcher m = p.matcher(str);
//拿着文本匹配器从头开始读取，寻找是否有满足规则的子串
//如果没有，方法会返回false
//如果有，会返回true，在底层记录子串的其实索引和结束索引 + 1
boolean b = m.find();
//方法底层会根据find方法记录的索引进行字符串的截取并返回
String s = m.group(index);//根据索引获取，因为正则表达式可能会分很多组，然后可以根据索引获取指定的那一组

```







## JDK7时间

###  `Date`类：

巴拉巴拉。。。。。。。



### `SimpleDateFormat`类作用：

格式化：把时间变成我们喜欢的格式。

解析：把字符串表示的时间变成Date对象。

| 构造方法                                  | 说明                                       |
| ----------------------------------------- | ------------------------------------------ |
| `public SimpleDateFormat()`               | 构造一个`SimpleDateFormat`，使用默认格式   |
| `public SimpleDateFormat(String pattern)` | 构造一个`SimpleDateFormat`，使用指定的格式 |



| 常用方法                                | 说明                           |
| --------------------------------------- | ------------------------------ |
| `public final String format(Date date)` | 格式化（日期对象  ->  字符串） |
| `public Date parse (String source)`     | 解析（字符串 -> 日期对象）     |



格式化的时间形式的常用的模式对应关系如下：

![](C:\Users\heban\AppData\Roaming\Typora\typora-user-images\image-20240402232243680.png)



下面是一些代码和注释方便理解：

```java
public static void main(String[] args) throws ParseException {

    //1.利用空参构造创建SimpleDataFormat对象
    SimpleDateFormat sdp = new SimpleDateFormat();//默认格式
    Date d1 = new Date(0L);
    String s1 = sdp.format(d1);
    System.out.println(s1);//输出结果：1970/1/1 08:00

    SimpleDateFormat sdp1 = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss EE");//指定格式
    String s2 = sdp1.format(d1);
    System.out.println(s2);//输出结果：1970年01月01日 08:00:00 周四

    //2.使用parse方法
    //定义一个字符串表示时间
    String str2 = "2023-11-11 11:11:11";
    //细节：创建的对象的格式要和字符串的格式一致
    SimpleDateFormat sdp2 = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");//格式一致
    //为了方便观察，这里又重复定义两个对象
    SimpleDateFormat sdp3 = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");//格式不一致
    SimpleDateFormat sdp4 = new SimpleDateFormat();//格式不一致
    //分别用三个不同格式的对象调用parse方法
    Date d2 = sdp2.parse(str2);
    System.out.println(d2);
    //以下定义会报错
    // Date d3 = sdp3.parse(str2);
    // Date d4 = sdp4.parse(str2);
    // System.out.println(d3);
    // System.out.println(d4);

}
```



如果最后那四行代码没有注释掉结果就会报错，如下图：

![image-20240404010016125](C:\Users\heban\AppData\Roaming\Typora\typora-user-images\image-20240404010016125.png)

则说明需要创建的对象的格式要和字符串的格式一致



练习代码：

```java
//肯打鸡秒杀
        //要求时间在下面的范围内
        String str1 = "2023年11月11日 00:00:00";
        String str3 = "2023年11月11日 00:10:00";

        String str4 = "2023年11月11日 00:01:00";//小贾同学抢购时间
        String str5 = "2023年11月11日 00:11:00";//小皮同学抢购时间
        
        SimpleDateFormat sdf7 = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");
        //
        Date start = sdf7.parse(str1);
        Date end = sdf7.parse(str3);
        long st = start.getTime();
        long et = end.getTime();
        //
        Date xj = sdf7.parse(str4);
        Date xp = sdf7.parse(str5);
        long xjt = xj.getTime();
        long xpt = xp.getTime();
       
        if(xjt >=st && xjt <= et)//秒杀成功
            System.out.println("秒杀成功");
        else
            System.out.println("秒杀失败");

        if(xpt >=st && xpt <= et)//秒杀失败
            System.out.println("秒杀成功");
        else
            System.out.println("秒杀失败");

        System.out.println("--------------------------------");

        //用正则表达式来解
        String regex = "2023年11月11日 00:(0\\d:[0-5]\\d)|(10:00)";
        if(str4.matches(regex))//秒杀成功
            System.out.println("秒杀成功");
        else
            System.out.println("秒杀失败");

        if(str5.matches(regex))//秒杀失败
            System.out.println("秒杀成功");
        else
            System.out.println("秒杀失败");


```

### `Calendar`类

概述：calendar类代表了系统当前的时间的日历对象，可以单独修改、获取时间中的年、月、日

- ==细节：Calendar是一个抽象类，不能直接创建对象==

#### 1.获取`Calendar`类日历对象的方法

| 方法名                                 | 说明                   |
| -------------------------------------- | ---------------------- |
| `public static Calendar getInstance()` | 获取当前时间的日历对象 |

#### 2.`Calendar`常用方法

| 方法名                                     | 说明                        |
| ------------------------------------------ | --------------------------- |
| `public final Date getTime()`              | 获取日期对象                |
| `public final setTime (Date date)`         | 给日历设置日期对象          |
| `public long getTimeInMillis()`            | 拿到时间毫秒值              |
| `public void setTimeInMillis(long millis)` | 给日历设置时间毫秒值        |
| `public int get(int field)`                | 取日历中的某个字段信息      |
| `public void set(int field,int value)`     | 修改日历中某个字段信息      |
| `public void add(int field,int amount)`    | 为某个字段增加/减少指定的值 |

注释：这里的amount修改不一定只是正数，也可以是负数



![image-20240405001910810](C:\Users\heban\AppData\Roaming\Typora\typora-user-images\image-20240405001910810.png)



```java
    public static void main(String[] args) throws ParseException {
            /* `public final Date getTime ()        获取日期对象
            public final setTime(Date date)         给日历设置日期对象

            | `public long getTimeInMillis ()`            |拿到时间毫秒值 |
            | `public void setTimeInMillis ( long millis)` |给日历设置时间毫秒值 |


            | `public int get ( int field)`                |取日历中的某个字段信息 |
            | `public void set ( int field, int value)`     |修改日历中某个字段信息 |
            | `public void add ( int field, int amount)`    |为某个字段增加 / 减少指定的值 |
            */

        Calendar c = Calendar.getInstance();
        //现在时间是2024-4-5-周五
        // c.set(Calendar.MONTH,5);//2024,6,5,星期三

        //amount为正表示向后加多少，为负则向前面减多少
        //而且月份你输入向后移动超过十二个月，java会自动把多余的转化为年份
        c.add(Calendar.YEAR, 1);//2025,4,5,星期六
        c.add(Calendar.MONTH, 1);//2024,5,5,星期日
        c.add(Calendar.MONTH, 13);//2025,5,5,星期一


        int year = c.get(Calendar.YEAR);
        int month = c.get(Calendar.MONTH) + 1;//月份是从0开始算起的
        int date = c.get(Calendar.DAY_OF_MONTH);
        int week = c.get(Calendar.DAY_OF_WEEK);//周数是从1开始的

        System.out.println(year + "," + month + "," + date + "," + week);//2024,4,5,6
        //如果想打印出星期数而不是数字可以写一个方法
        System.out.println(year + "," + month + "," + date + "," + getWeek(week));//2024,4,5,星期五
    }

    public static String getWeek(int week) {
        String[] w = {"", "星期日", "星期一", "星期二", "星期三", "星期四", "星期五", "星期六"};

        return w[week];
    }

```



`Calendar`类总结：

![image-20240405001807804](C:\Users\heban\AppData\Roaming\Typora\typora-user-images\image-20240405001807804.png)



## JDK8时间

JDK8时间类中月份就是按1 ~ 12来的，不是0 ~ 11.



### `Data`类



![image-20240405222426533](C:\Users\heban\AppData\Roaming\Typora\typora-user-images\image-20240405222426533.png)



#### `ZoneId`：时区



| 方法名                                     | 说明                     |
| ------------------------------------------ | ------------------------ |
| `static Set<String> getAvailableZoneIds()` | 获取java中支持的所有时区 |
| `static ZoneId systemDefault()`            | 获取系统默认的时区       |
| `static ZoneId of(String zoneId)`          | 获取一个指定的时区       |

==注：Set<String>是一个集合==



```java
Set<String> ss = ZoneId.getAvailableZoneIds();
System.out.println(ss);//600个时区

ZoneId z1 = ZoneId.systemDefault();
System.out.println(z1);//Asia/Shanghai

ZoneId a2 = ZoneId.of("Asia/Aden");
System.out.println(a2);//Asia/Aden

```



#### `Instant`：时间戳



![image-20240406001855691](C:\Users\heban\AppData\Roaming\Typora\typora-user-images\image-20240406001855691.png)



#### `AoneDataTime`：带时区的时间



![image-20240406002027021](C:\Users\heban\AppData\Roaming\Typora\typora-user-images\image-20240406002027021.png)



==细节：==

==JDK8新增的时间对象是不可变的，如果修改了（增加、减少），调用者是不会发生改变的，会产生一个新的时间==



### 日期格式化类



![image-20240406001441437](C:\Users\heban\AppData\Roaming\Typora\typora-user-images\image-20240406001441437.png)



### 日历类



#### `LocalDate`：年、月、日

#### `LocalTime`：时、分、秒

#### `LocalDateTime`：年、月、日、时、分、秒

![image-20240406152946195](C:\Users\heban\AppData\Roaming\Typora\typora-user-images\image-20240406152946195.png)



部分代码练习：

```java
        LocalDate now = LocalDate.now();
        System.out.println(now);//2024-04-06

        LocalDate l1 = now.plusDays(10);//在原来的日期上加十天。
        System.out.println(l1);//2024-04-16
```



### 工具类



#### `Duration`:时间间隔（秒、纳秒）

#### `Period`：时间间隔（年、月、日）

#### `ChronoUnit`:时间间隔（所有单位）

练习代码：

```java
		//现在时间
        LocalDateTime today = LocalDateTime.now();
        System.out.println(today);//2024-04-06T15:32:40.720884800
        //指定时间
        LocalDateTime birthDay = LocalDateTime.of(2005, 4, 8, 0, 0, 0);
        System.out.println(birthDay);//2005-04-08T00:00
        //计算时间间隔的方法
        //第二个减第一个
        System.out.println("相差的年数：" + ChronoUnit.YEARS.between(birthDay,today));//相差的年数：18
        System.out.println("相差的月数：" + ChronoUnit.MONTHS.between(birthDay,today));//相差的月数：227
        System.out.println("相差的周数：" + ChronoUnit.WEEKS.between(birthDay,today));//相差的周数：991
        System.out.println("相差的天数：" + ChronoUnit.DAYS.between(birthDay,today));//相差的天数：6938
        System.out.println("相差的时数：" + ChronoUnit.HOURS.between(birthDay,today));//相差的时数：166528
        System.out.println("相差的分数：" + ChronoUnit.MINUTES.between(birthDay,today));//相差的分数：9991687
        System.out.println("相差的秒数：" + ChronoUnit.SECONDS.between(birthDay,today));//相差的秒数：599501221
        System.out.println("相差的毫秒数：" + ChronoUnit.MILLIS.between(birthDay,today));//相差的毫秒数：599501221728
        System.out.println("相差的微秒数：" + ChronoUnit.MICROS.between(birthDay,today));//相差的微秒数：599501221728226
        System.out.println("相差的纳秒数：" + ChronoUnit.NANOS.between(birthDay,today));//相差的纳秒数：599501221728226500
        System.out.println("相差的半天数：" + ChronoUnit.HALF_DAYS.between(birthDay,today));//相差的半天数：13877
        System.out.println("相差的十年数：" + ChronoUnit.DECADES.between(birthDay,today));//相差的十年数：1
        System.out.println("相差的世纪（百年）数：" + ChronoUnit.CENTURIES.between(birthDay,today));//相差的世纪（百年）数：0
        System.out.println("相差的千年数：" + ChronoUnit.MILLENNIA.between(birthDay,today));//相差的千年数：0
        System.out.println("相差的纪元数：" + ChronoUnit.ERAS.between(birthDay,today));//相差的纪元数：0

```



---------------



# 四、泛型程序设计



## 解释一些概念



### **参数化类型**

指的是带有具体泛型参数的类型。简单来说，参数化类型就是指那些在泛型类或接口中，用具体的类型替换了泛型参数的类型。

定义一个类：

``` java
public class Box<T>{
    //...
}

//现在new 两个Box对象
Box<String> stringBox = new Box<>();
Box<Integer> integerBox = new Box<>();
```

在上面的`Box<String>`和`Box<Integer>`就是两个参数化类型，这里面泛型就是参数，`Box<String>`表示的是一个`Box`类型，但是其中泛型参数`T`被具体化成一个`Stirng`类型

==**在获取参数化类型时，获取的是直接类的类型**==，也就是说获取的不是泛型类型，而是带有泛型参数的类的类型

那上面的类型举例子，获取的是Box类，而不是Box中的泛型 T 类型（不是String、Integer类型）









泛型：是JDK5引入的特性，可以在编译阶段约束操作的数据类型，并进行检查。

泛型的格式：<数据类型>

==注意 ： 泛型只能支持引用数据类型==



==拓展：==

如果我们没有给集合指定类型，默认认为所有的类型时object类型

此时可以往集合中添加任何数据类型

这样会带来一个坏处：我们在获取数据类型的时侯，不可以调用它的特有行为，如果想调用可以强转，但是强转很容易引发类型转化异常

此时推出了泛型，可以在添加数据的时候就把数据类型统一，在获取数据类型的时候省去了强转

```java
		//创建一个没有使用泛型的集合	   
	    ArrayList list = new ArrayList();
        //添加数据
        list.add("aaa");//添加字符串
        list.add(123);//添加整数
        list.add(123.3);//添加浮点数
        //打印集合
        Iterator it = list.iterator();
        while (it.hasNext()) {
            Object obj = it.next();
            //多态的弊端是不能调用子类的特有功能
            //obj.length();这么写会报错
            //如果是想用子类的特有功能，只能是将object强转为子类
            /*
            String str = (String)it.next();
            str.length();这么写不会报错
            但是如果这么写，会认为所有添加的数据都是string类型，但是有些类型不能强转为string类
            在打印时会报错
            */
            System.out.println(obj);
        }

```



==拓展知识点== ： Java中的泛型是伪泛型



==泛型的细节==

- 泛型中不能写基本数据类型，
- 指定泛型的具体类型后，传递数据时，可以传入该类类型或者其子类类型
- 如果不写泛型，类型默认时Object



## 1.泛型类

使用场景：当一个类中，某个变量的数据类型不能确定时，就可以定义带有泛型的类

格式：

修饰符 class 类名 <类型>{

}

```java
public class ArrayList<E>{
	//
}
```

字母可以使用   E、K、V、T



## 2.泛型方法

泛型可以放在两个地方

1. 使用类名后面定义的泛型 ---------------> 所有方法都可以使用
2. 在方法申明上定义自己的泛型---------->只有本方法可以使用

```java
public static <E> void method(ArrayList<E> list){...}
```





## 3.泛型接口



如何使用一个带泛型的接口

1. 在实现类中给出具体类型

   ```java
   //自己定义的一个集合
   public class MyArrayList implements List<String> {...}
   ```

   

   ```java
   MyArrayList list = new MyArrayList();
   //这里就不用给出MyArrayList存放数据的类型了，因为在实现类中已经确定了List泛型为<String>
   list.add("aaa");//这样可以
   list.add(123);//这样是错误的
   ```

   

2. 实现类延续泛型，创建对象时再确定

   ```java
   public class MyArrayList<E> implements List<E> {...}
   ```

   ```java
   MyArrayList<String> list = new MyArrayList<>();//这里就要给出类型了
   ```

   

## 4.泛型的通配符

### 大致作用和格式：

​	利用泛型方法有一个小弊端：就是可以接受任意的数据类型

​	但是如果要求是不确定类型，但是希望只能是传递 `Ye Fu Zi`

​	此时就可以使用泛型的通配符

​				?也可以表示不确定的类型

​				它可以进行类型的限定

​				? extends E : 表示可以传递E或者E所有的子类类型

​				? super E : 表示可以传递E或者E的所有父类类型

```java
public static void method(ArrayList<? extends Ye> list){...}
//这里只能传入Ye类型或者Ye的子类类型
```



```java
public static void method(ArrayList<? super Fu> list){...}
//此时只能添加Fu类型或者Ye类型，Zi类型就不能添加了
```



### 应用场景：

1. 如果我们在定义类、方法、接口的时候，如果类型不确定，就可以定义泛型类、泛型方法、泛型接口
2. 如果类型不确定，但是能知道以后只能传递某个继承体系中的类型，就可以使用泛型的通配符

### 关键点：  

可以限定类型的范围

### 泛型的通配符练习代码

这些类应该一个一个的定义的，而不是全部在一个类中

```java
import java.text.ParseException;
import java.util.ArrayList;

public class text {
    public static void main(String[] args) throws ParseException {
        ArrayList<dog> list = new ArrayList<>();
        Husky hk = new Husky("二哈", 2);
        teddy td = new teddy("小哈"，1);
        list.add(hk);
	    list.add(td);
        keepPet1(list);
        //一只叫做二哈的2岁的哈士奇，正在吃骨头，边吃边拆家
	   //一只叫做小哈的1岁的泰迪，正在吃骨头，边吃边蹭
	
    }

    //方法一，能养所有的狗，但不能养猫
    public static void keepPet1(ArrayList<? extends dog> list) {
        for (dog dog : list) {
            dog.eat();
        }
    }

    //方法二，能养所有的猫，但不能养狗
    public static void keepPet2(ArrayList<? extends cat> list) {
        for (cat cat : list) {
            cat.eat();
        }
    }

    //方法三，能养所有动物
    public static void keepPet3(ArrayList<animal> list) {
        for (animal animal : list) {
            animal.eat();
        }
    }

}

//定义一个动物类
abstract class animal {
    private String name;
    private int age;

    public animal() {
    }

    public animal(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public abstract void eat();

    /**
     * 获取
     *
     * @return name
     */
    public String getName() {
        return name;
    }

    /**
     * 设置
     *
     * @param name
     */
    public void setName(String name) {
        this.name = name;
    }

    /**
     * 获取
     *
     * @return age
     */
    public int getAge() {
        return age;
    }

    /**
     * 设置
     *
     * @param age
     */
    public void setAge(int age) {
        this.age = age;
    }

    public String toString() {
        return "animal{name = " + name + ", age = " + age + "}";
    }

}

//定义一个抽象猫类
abstract class cat extends animal {

    public cat() {
    }

    public cat(String name, int age) {
        super(name, age);
    }

}

//定义一个抽象狗类
abstract class dog extends animal {
    public dog() {
    }

    public dog(String name, int age) {
        super(name, age);
    }
}

//定义一个波斯猫类
class perSian extends cat {
    public perSian() {
    }

    public perSian(String name, int age) {
        super(name, age);
    }

    @Override
    public void eat() {
        System.out.println("一只叫做" + getName() + "的" + getAge() + "岁的波斯猫，正在吃小饼干");
    }

}

//定义一个狸花猫类
class liHua extends cat {


    public liHua() {
    }

    public liHua(String name, int age) {
        super(name, age);
    }

    @Override
    public void eat() {
        System.out.println("一只叫做" + getName() + "的" + getAge() + "岁的狸花猫，正在吃鱼");
    }

}

//定义一个泰迪类
class teddy extends dog {


    public teddy() {
    }

    public teddy(String name, int age) {
        super(name, age);
    }

    @Override
    public void eat() {
        System.out.println("一只叫做" + getName() + "的" + getAge() + "岁的泰迪，正在吃骨头，边吃边蹭");
    }

}

//定义一个哈士奇类
class Husky extends dog {

    public Husky() {
    }

    public Husky(String name, int age) {
        super(name, age);
    }

    @Override
    public void eat() {
        System.out.println("一只叫做" + getName() + "的" + getAge() + "岁的哈士奇，正在吃骨头，边吃边拆家");
    }

}

```





## 泛型的擦除机制

Java 泛型是一种编译时的特性，主要用于提供类型安全和代码复用。然而，泛型信息在运行时会被擦除（Type Erasure），这意味着运行时的字节码中不会保留泛型的具体类型信息。例如：

```java
List<String> list = new ArrayList<>();
```

在运行时，`List<String>` 会被处理为 `List`，泛型参数 `String` 的信息会被擦除。



#### 如何避免泛型擦除

##### 	使用匿名子类

​	通过创建一个匿名子类，可以绕过类型擦除的限制。匿名子类的定义会保留泛型参数的类型信息，使得反射机制能够获取到这些信息。

​	当创建一个`Box<T>`的匿名子类的时候编译器会生成类似下面的类：

``` java
class Main$1 extends Box<List<String>> {
}
```









# 五、异常



异常：异常就是代表程序出现的问题

异常体系的最上层父类是`Exception`,异常分为两类，一类是编译时异常，另一类是运行时异常

编译时异常和运行时异常的区别

- 编译时异常：
  	没有继承`RuntimeException`的异常，直接继承于`Exception`。编译阶段就会错误提示

- 运行时异常：
   `RuntimeException`本身和子类，编译阶段没有错误提示，运行时出现的



## 作用

- 作用一：异常时用来查询bug的关键参考信息
- 作用二：异常可以作为方法内部的一种特殊返回值，以便通知调用者底层的执行情况



## 异常中的常见方法

Throwable的成员方法

| 方法名称                        | 说明                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| `public String getMessage()`    | 返回此throwable的详细消息字符串                              |
| `public String toString()`      | 返回此可抛出的简短描述                                       |
| `public void printStackTrace()` | 底层利用`System.err.println()`进行输出，把异常的错误信息以红色字体输出在控制台，仅仅是打印信息，<br />不会停止程序的运行 |



```java
package com.hnust.student;

public class text {
    public static void main(String[] args) {
        int[] arr = {1,2,3,4,5,6,7,8,9};

        try {
            System.out.println(arr[10]);
        } catch (ArrayIndexOutOfBoundsException e) {
            String message = e.getMessage();
            System.out.println(message);//Index 10 out of bounds for length 9

            String string = e.toString();
            System.out.println(string);//java.lang.ArrayIndexOutOfBoundsException: Index 10 out of bounds for length 9

            e.printStackTrace();

        }

        System.out.println("看看我执行了没");

    }
}

/*
Index 10 out of bounds for length 9
java.lang.ArrayIndexOutOfBoundsException: Index 10 out of bounds for length 9
看看我执行了没
java.lang.ArrayIndexOutOfBoundsException: Index 10 out of bounds for length 9
	at com.hnust.student.text.main(text.java:8)

*/
```





## 异常的处理方式



### 1.`JVM`默认的处理方式

- 把异常的名称、异常的原因以及异常的出现位置等信息输出在控制台
- 程序停止执行，下面的代码不会再执行了

### 2.自己处理（捕获异常）

格式

```java
try{
	可能出现异常的代码;
} catch(异常类名 变量名) {
	异常的处理代码;
} finally {
    //特点：finally里面的代码一定会执行，除非虚拟机停止
}
```

目的：当代码出现异常的时候，可以让程序继续往下执行。



#### **思考**

1. 如果try种没有遇到问题，会怎么执行？

   ```java
   package com.hnust.student;
   
   public class text {
       public static void main(String[] args) {
           int[] arr = {1,2,3,4,5,6,7,8,9};
   
           try{
               System.out.println(arr[0]);
           }catch(ArrayIndexOutOfBoundsException e){
               System.out.println("数组索引越界了");
           }
   
           System.out.println("看看我执行了没");
   
       }
   }
   /*
   1
   看看我执行了没
   */
   
   ```

   会把try里面所有的代码执行完毕，不会执行catch里面的代码

   只有出现了异常才会执行catch里面的代码

   

2. 如果try中可能会遇到很多问题，会怎么执行？

   ```java
   package com.hnust.student;
   
   public class text {
       public static void main(String[] args) {
           int[] arr = {1,2,3,4,5,6,7,8,9};
   
           try{
               System.out.println(arr[10]);//ArrayIndexOutOfBoundsException
               System.out.println(2/0);//ArithmeticException
           }catch(ArrayIndexOutOfBoundsException e){
               System.out.println("数组索引越界了");
           }catch (ArithmeticException e){
               System.out.println("除数异常");
           }
   
           System.out.println("看看我执行了没");
           
       }
   }
   /*
   数组索引越界了
   看看我执行了没
   */
   ```

   这就需要写多个catch与之对应

   ==细节== ：如果需要捕获多个异常，这些异常中如果存在父子关系的话，那么父类一定要写在后面，因为如果把父类写在子类前面那么子类在从上往下匹配catch时会直接进入父类的catch中，而不会进入自己的那个catch中。即使子类出现了异常，子类的那个catch也不会执行。

   

   

   

3. 如果`try`中遇到的问题没有被捕获，会怎么执行？

   相当于try{...}catch{...}的代码白写了，最终还是会交给虚拟机进行处理（JVM默认的处理方式）

   

4. 如果try中遇到了问题，那么try下面的其他代码还会执行吗？

   ```java
   package com.hnust.student;
   
   public class text {
       public static void main(String[] args) {
           int[] arr = {1,2,3,4,5,6,7,8,9};
   
           try{
               System.out.println(arr[10]);//ArrayIndexOutOfBoundsException
               System.out.println("看看我执行了没？？？？？");//ArithmeticException
           }catch(ArrayIndexOutOfBoundsException e){
               System.out.println("数组索引越界了");
           }catch (ArithmeticException e){
               System.out.println("除数异常");
           }
   
           System.out.println("看看我执行了没");
           
       }
   }
   ```

   try中遇到问题后面的代码就不会执行了，直接跳转到相应的catch当中，执行catch里面的语句体

   但是如果没有与之匹配的catch，还是会交给虚拟机进行处理（JVM默认处理方式）

5. finaly语句中代码执行情况

   ``` java
   try {
       return "try!";
   } finally {
       return "finally!";
   }
   //这串代码返回的字符串是“finally!”，而不是“try！”
   //因为finally块总是会在try块和catch块执行完毕后执行，无论try块中是否发生了异常，或者try块中是否执行了return语句。
   ```

   



### 3.抛出异常

#### `throws`

注意：写在方法定义（方法声明）处，表示声明一个异常，告诉调用者，使用本方法可能会有哪些异常，但是在本方法中不会去处理这个异常

```java
public void 方法()throws 异常类名1,异常类名2...{
    
}
```

- 编译时异常：必须写上
- 运行时异常：可以不写



#### `throw`

注意：可以在方法的任何地方使用，写在方法内，结束方法，手动抛出异常对象，交给调用者，方法中下面的代码就不再执行了

```java
public void 方法(){
	throw new 异常类名();
}
```



## 自定义异常

1. 定义异常类
2. 写继承关系
3. 空参构造
4. 带参构造

意义：就是为了让控制台的报错信息更加的见名知意

```java
//名字异常
public class NameFormatException extends RuntimeException{
    //技巧
    //NameFormat 当前异常的名字，表示姓名格式化问题
    //Exception 表示当前是一个异常类
    
    //异常又分为两种
    //运行时异常：RuntimeException 核心 就表示由于参数错误导致的问题
    //编译时异常：Exception 核心 提醒程序员检查本地的信息
    
    public NameFormatException(){
    }

    public NameFormatException(String message){
        super(message);
    }
    /*
    */
}
```



```java
//年龄异常
public AgeOutOfBoundsException extends RuntimeException{
    public AgeOutOfBoundsException(){
    }
    
    public AgeOutOfBoundsException(String message){
    super(message);
    }
    
}
```



异常的构造方法可以包含不同的参数，这些参数用于提供关于异常的额外信息，以便更好地理解和处理异常。以下是一些常见的参数及其含义：

1. **Throwable cause**：这是最常见的参数之一，它表示导致当前异常的另一个异常（原因）。这个参数允许异常链的创建，即一个异常可以包含导致它的另一个异常的引用。这有助于调试，因为它提供了异常发生的上下文。
2. **String message**：这个参数是一个字符串，提供了关于异常的简短描述。这个描述通常是对异常情况的人类可读的解释。
3. **boolean enableSuppression** 和 **boolean writableStackTrace**：这两个参数是Java 7引入的，用于控制异常的某些行为。enableSuppression 参数允许应用程序通过调用 Throwable.addSuppressed 方法来抑制其他异常。writableStackTrace 参数决定是否允许将堆栈跟踪转换为字符串，这对于调试非常有用。
4. **`StackTraceElement[] stackTraceElements`**：这是一个可选参数，它允许你提供一个自定义的堆栈跟踪数组。这在某些情况下很有用，比如当你想要修改异常的堆栈跟踪信息时。







## Error类

- `Error`类代表了Java运行时环境遇到的严重问题。这些问题通常是程序无法处理的，例如内存溢出、线程死亡或虚拟机错误。`Error`类通常指示的是程序运行环境的问题，而不是程序逻辑错误。

- 通常不需要捕获或处理。它们是不可恢复的，程序在遇到`Error`时通常会终止。

- 是`Throwable`类的直接子类，它通常不被用户程序直接使用，而是由Java运行时系统抛出。

- 用于表示程序运行时环境的严重错误，如`OutOfMemoryError`、`StackOverflowError`等。



#### Error类和Exception类的区别

Error类：代表了程序运行时的严重错误，通常都不需要捕获和处理，程序在遇到Error类时通常会直接终止

Exception类：代表了程序中可预料到的异常情况，是可以被捕获和处理的，用于指示程序逻辑错误或者外部环境问题。





# 六、File



- File对象就表示一个路径，可以是文件的路径，也可以是文件夹的路径
- 这个路径可以是存在的，也可以是不存在的



绝对路径是带盘符的，相对路径是不带盘符的，默认到当前项目下去找



## 文件中的常见方法



### 构造方法

| 方法名称                                   | 说明                                               |
| ------------------------------------------ | -------------------------------------------------- |
| `public File(String pathname)`             | 根据文件路径创建文件对象                           |
| `public File(String parent, String child)` | 根据父路径名 字符串和子路径名 字符串创建文件对象   |
| `public File(File parent, String child)`   | 根据父路径对应文件对象和子路径名字符串创建文件对象 |



```java
package com.hnust.student;

import java.io.File;

public class text {
    public static void main(String[] args) {

        //1.根据字符串表示的路径，变成File对象
        String str = "C:\\Users\\heban\\Desktop\\a.txt";
        File file1 = new File(str);
        System.out.println(file1);//C:\Users\heban\Desktop\a.txt
        
        System.out.println("------------------------------------");

        //2.父级路径：C:\Users\heban\Desktop
        //子级路径：a.txt
        String parent = "C:\\Users\\heban\\Desktop";
        String child = "a.txt";
        File file2 = new File(parent, child);
        System.out.println(file2);//C:\Users\heban\Desktop\a.txt

        System.out.println("------------------------------------");
        
        File parent1 = new File("C:\\Users\\heban\\Desktop");
        String child1 = "a.txt";
        File file4 = new File(parent1,child1);
        System.out.println(file4);//C:\Users\heban\Desktop\a.txt


    }
}
```





### 常见成员方法



| 方法名称                          | 说明                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| `public boolean isDirectory()`    | 判断此路径名表示的File是否为文件夹                           |
| `public boolean isFile()`         | 判断此路径名表示的File是否为文件                             |
| `public boolean exists()`         | 判断此路径名表示的File是否存在                               |
| `public long length()`            | 返回文件的大小 (字节数量)                                    |
| `public String getAbsolutePath()` | 返回文件的绝对路径                                           |
| `public String getPath()`         | 返回定义文件时使用的路径，当时创建对象时括号里面的参数是什么就会返回什么 |
| `public String getName()`         | 返回文件的名称，带后缀名（拓展名），如果是文件夹，则返回文件夹的名称 |
| `public long lastModified()`      | 返回文件的最后修改时间（时间毫秒值）                         |



#### `length`方法

- 细节1：这个方法只能获取文件的大小，单位是字节
- 细节2：这个方法无法获取文件夹的大小，如果要获取文件夹的大小，需要把文件夹里面的所有文件累加在一起





| 方法名称                         | 说明                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| `public boolean createNewFile()` | 创建一个新的空的文件                                         |
| `public boolean mkdir()`         | 创建单级文件夹                                               |
| `public boolean mkdirs()`        | 创建多级文件夹                                               |
| `public boolean delete()`        | 夹删除文件、空文件夹，`delete`方法默认只能删除文件和空文件夹，`delete`方法直接删除不走回收站 |
| `public File[] listFiles()`      | 获取当前该路径下所有的内容，以数组的形式返回                 |



#### `createNewFile`细节

- 细节1：如果当前路径表示的文件是不存在的，则创建成功，方法返回true。

  ​			如果当前路径表示的文件是存在的，则创建失败，方法返回false。

- 细节2：如果父级路径是不存在的，那么方法会有异常`IOException`

- 细节3：`createNewFile`方法创建的一定是文件，如果路径中不包含后缀名，则创建一个没有后缀名的文件



#### `mkdir`方法

`mkdir` --->  make Directory 文件夹（目录）

细节1：`windows`当中路径是唯一的，如果当前路径已经存在，则创建失败，返回false

细节2：`mkdir`方法只能创建单级文件夹，无法创建多级文件夹



#### `mkdirs`方法

细节：既可以创建多级文件夹，也可以创建单级文件夹，如果文件是存在的，那么创建失败，如果文件是不存在的，则创建成功。



#### `delete`方法

细节：如果删除的是文件，则直接删除，不走回收站

​			如果删除的是空文件夹，则直接删除，不走回收站

​			如果删除的是有内容的文件夹，则删除失败



### `listFiles`方法

- 当调用者`File`表示的路径不存在时，返回null
- 当调用者`File`表示的路径是文件时，返回null
- 当调用者`File`表示的路径是一个空文件夹时，返回一个长度为零的数组
- 当调用者`File`表示的路径是一个有内容的文件夹时，将里面所有的文件夹和文件的路径放在`File`数组中并返回
- 当调用者`File`表示的路径是一个有隐藏文件的文件夹时，将里面所有的文件夹和文件的路径放在`File`数组中返回，包包含隐藏文件
- 当调用者`File`表示的路径是需要权限才能访问的文件夹时，返回null



==注意== ： `File`类只能对文件本身进行操作，==不能读写文件里面存储的数据==。

# `IO`流

## 初步了解

`IO`流：存储和读取数据的解决方案

  作用：用于读写文件中的数据（可以读写文件或网络中的数据······）

把程序中的数据保存到文件中--->写（output)

把本地文件加载到程序中-->读（input）



问：`IO`流中，谁在读，谁在写，以谁为参照物看读写的方向呢？

是以程序（内存）作为参照物的。



## `IO`流的分类

### `IO`流按照流向分可以分为两种流

- 输出流：程序--->文件
- 输入流：文件--->程序



### `IO`流按照操作文件类型可以分为两种

- 字节流：可以操作所有类型的文件

  - `InputStream`(抽象类)

    `FileInputStream`,操作本地文件的字节输入流

  - `OutputStream`(抽象类)

    `FileOutputStream`,操作本地文件的字节输出流

    

- 字符流：只能操作纯文本文件

  - `Reader`(抽象类)

    `FileReader`,操作本地文件的字符输入流

  - `Writer`(抽象类)

    `FileWrite`,操作本地文件的字符输出流



纯文本文件：用windows系统自带的记事本打开并且能够读懂的文件，例如： txt文件、md文件、xml文件、`lrc`文件等



#### 字节流



##### 基础流

###### `FileOutputStram`  

```
		--->  操作本地文件的字节输出流，可以把程序中的数据写入到本地文件中，是字节流的基本流
```



书写步骤

1. 创建字节输出流对象

   细节1：参数是字符串表示的路径或者是File表示的对象都是可以的

   ```java
   //有两种构造方法
   
   //构造方法1------->File对象构造
   public FileOutputStream(File file) throws FileNotFoundException {
           this(file, false);
       }
   //构造方法2---->字符串构造
    public FileOutputStream(String name) throws FileNotFoundException {
           this(name != null ? new File(name) : null, false);
       }
   
   //其实还有一个，可以传递两个参数，第一个参数就是字符串，第二个参数表示是否开启续写
   //true表示开启续写，false表示关闭续写
   public FileOutputStream(String name, boolean append)
           throws FileNotFoundException
       {
           this(name != null ? new File(name) : null, append);
       }
   
   ```

   细节2：如果文件不存在则会创建一个新的文件，但是要保证父级路径是存在的，如果父级路径也不存在，则会报错

   细节3：如果文件已经存在，则会清空文件中的内容 

   

2. 写数据
   细节：`write`方法的参数是整数，但实际上写到本地文件中的是整数在ASCII上对应的字符

   ```java
   public void write(int b) throws IOException {
           boolean append = FD_ACCESS.getAppend(fd);
           long comp = Blocker.begin();
           try {
               write(b, append);
           } finally {
               Blocker.end(comp);
           }
       }
   
   ```

   

3. 释放资源

   细节：每次使用完流之后都要释放资源，作用就是解除对本地文件的占用，如果不释放的话`java`程序就会一直占用着文件，占用文件期间是不能不文件进行操作的，比如不能删除文件。所以释放资源是解除对本地文件的占用

   ==细节== ： ==先开的流后关闭==

   

```java
//1.创建对象
FileOutputStream fos= new FileOutputStream("C:\\develop\\practiceOfFileAndIO\\a.txt");
//2.写出数据
fos.write(97);
//3.释放资源
fos.close();

//程序就是从第一行代码中的C:\\develop\\practiceOfFileAndIO\\a.txt路径与本地文件产生一个数据传输通道
//通过write把数据传输到本地文件
//最后用close关闭通道
```



`FileOutputStream`写数据的三种方式

| 方法名称                                 | 说明                                                         |
| ---------------------------------------- | ------------------------------------------------------------ |
| `void write(int b)`                      | 一次写一个字节数据                                           |
| `void write(byte[] b)`                   | 一次写一个字节数组数据                                       |
| `void write(byte[] b, int off, int len)` | 一次写一个字节数组的部分数据，<br />参数一 ---> 字节数组<br / >参数二 ---> 起始索引<br />参数三 ---> 传入个数 |





换行写

​	写出一个换行符就可以了
​	windows ： 	\r\n
​	Linux : 			\n
​	Mac :			   \r 

细节：在windows操作系统中，java对回车换行进行了优化，虽然完整的是`\r\n`，但是我们写其中一个\r或者\n

java也可以实现换行，因为java在底层会补全

建议：

​	不要省略，还是写全比较好

​	

续写

​	如果想要续写，打开续写开关即可

​	开关位置：创建对象的第二个参数

​	手动传递true，表示打开续写，此时创建的对象不会清空文件



```java
public static void main(String[] args) throws IOException {
    //1.创建对象
    FileOutputStream fos= new FileOutputStream("C:\\develop\\practiceOfFileAndIO\\a.txt",false);
    //如果想续写的话就直接把第二个参数改为true就行了

    //2.写出数据
    String str1 = "hebangchenzhengshuai";
    byte[] bytes1 = str1.getBytes();
    fos.write(bytes1);
    //写换行符
    String str2 = "\r\n";
    byte[] bytes2 = str2.getBytes();
    fos.write(bytes2);

    String str3 = "666";
    byte[] bytes3 = str3.getBytes();
    fos.write(bytes3);

    //3.释放资源
    fos.close();

    /*
    * hebangchenzhengshuai
    * 666
    */
    
}
```



###### `FileInputSream`

----->操作本地文件的字节输入流，可以把本地文件的数据读取到程序中来



书写步骤

1. 创建字节输入流对象
   细节1：如果文件不存在就会直接报错
   java为什么会这么设计呢？

   输出流：不存在，创建一个新的文件
   				并把数据写到文件中
   输入流：不存在，直接报错
   			因为创建出来的文件是没有数据的，没有任何意义
   			所以java就没有设计出这种无意义的逻辑，文件不存在直接报错

   

   程序中最重要的是 ==数据==

   

2. 读数据

   细节1：一次只读一个字节，读出来的是数据在ASCII上对应的数字

   细节2：读到文件末尾了，read方法返回-1；

   | 方法名称                         | 说明                                                         |
   | -------------------------------- | ------------------------------------------------------------ |
   | `public int read()`              | 一次读一个字节的数据                                         |
   | `public int read(byte[] buffer)` | 一次读一个字节数组的数据，返回值是本次读取读到了多少字节数据 |

   

   注意：一次读一个字节数组的数据，每次读取会尽可能把数组装满，创建数组时一般会默认创建1024的整数倍。

   

   

   

3. 释放资源

   细节：每次使用完流之后都要释放资源



循环读取

```java
//创建字节输入流的对象
FileInputStream fis = new FileInputStream("C:\\develop\\practiceOfFileAndIO\\a.txt");

//读数据
int c;
while((c = fis.read()) != -1){
    System.out.print((char)c);
}

//释放资源
fis.close();
```



在特定情况下实现接口`AutoCloseable`可以自动释放







#### 字符流

字符流 = 字节流 + 字符集

字符流底层其实就是字节流

##### 特点

输入流：一次读一个字节，遇到中文时，一次读多个字节

输出流：底层会把数据按照指定的编码方式进行编码，变成字节再写到文件中



##### 使用场景

对于文本文件进行读写操作



##### `FileReader`

1. 创建字符输入流的对象

   | 构造方法                             | 说明                       |
   | ------------------------------------ | -------------------------- |
   | `public FileReader(File file)`       | 创建字符输入流关联本地文件 |
   | `public FileReader(String pathname)` | 创建字符输入流关联本地文件 |

   细节：如果读取文件不存在，则会直接报错

   

2. 读取数据

   | 成员方法                         | 说明                         |
   | -------------------------------- | ---------------------------- |
   | `public int read()`              | 读取数据，读到末尾返回-1     |
   | `public int read(char[] buffer)` | 读取多个数据，读到末尾返回-1 |

   细节1：按字节进行读取，遇到中文，一次读取多个字节，读取后解码，返回一个整数（十进制）

   ​			GBK一次读取两个字节，UTF-8一次读取三个字节，

   细节2：读到文件末尾了，read方法返回-1

   

3. 释放资源



| 成员方法             | 说明          |
| -------------------- | ------------- |
| `public int close()` | 释放资源/关流 |



##### 字符流原理解析

1. 创建字符输入（出）流对象

   底层：关联文件，并创建缓冲区（就是长度为8192的字节数组）
   创建字符输入流时才会创建缓冲区，创建字节输入流时是不会创建缓冲区的

2. 读取对象

   底层：

   1. 判断缓冲区是否有数据可以读取

   2. 缓冲区中没有数据：就从文件中获取数据，装到缓冲区中，每次尽可能装满缓冲区
          如果文件中没有数据了，就会返回-1；

   3. 缓冲区中有数据：就从缓冲区中读取。

      空参的read方法：一次读取一个字节，遇到中文一次读多个字节，把字节解码并转化成十进制返回

      有参的read方法：把读取字节、解码、强转三步合并了，强转之后的字符放到数组中

   

   

   | 成员方法              | 说明                             |
   | --------------------- | -------------------------------- |
   | `public void flush()` | 将缓冲区中的数据刷新到本地文件中 |

   ==细节== ： flush刷新后还可以继续往文件中写入数据，而close方法关流后就不能继续往本地文件中写入数据



#### 字节流和字符流有什么区别？



1. **数据单位不同**：
   - **字节流**：以字节（8位）为单位进行数据的读写。字节流是面向字节的，它处理的是原始的二进制数据，不关心数据的含义。
   - **字符流**：以字符（16位）为单位进行数据的读写。字符流是面向字符的，它处理的是文本数据，通常用于处理文本文件。
2. **编码方式不同**：
   - **字节流**：不涉及字符编码转换，直接读写原始字节数据。
   - **字符流**：涉及到字符编码转换，通常使用平台默认的字符编码（如UTF-8、GBK等），在读写文件时会将字符编码转换为字节，或反之。
3. **类继承不同**：
   - **字节流**：继承自`java.io.InputStream`和`java.io.OutputStream`类。
   - **字符流**：继承自`java.io.Reader`和`java.io.Writer`类。
4. **使用场景不同**：
   - **字节流**：适合处理二进制文件，如图片、音频、视频等。
   - **字符流**：适合处理文本文件，如.txt、.csv、.xml等。
5. **性能考虑**：
   - **字节流**：通常比字符流快，因为它处理的是原始的二进制数据，不需要进行编码转换。
   - **字符流**：由于涉及到编码转换，可能会比字节流慢一些，但在处理文本数据时更加方便和安全。
6. **异常处理**：
   - **字节流**：使用`IOException`。
   - **字符流**：使用`IOException`和`UnsupportedEncodingException`。









## 缓冲流

缓冲流可以提高读写的效率



### 字节缓冲流

原理：底层自带了长度为8192的缓冲区提高性能

==注意== ： 在字节缓冲==输入==流中，创建的是大小为8192的==字节==数组

而在字符缓冲==输出==流中，创建的是大小为8192的==字符==数组（一个char占两个字节）

| 方法名称                                       | 说明                                     |
| ---------------------------------------------- | ---------------------------------------- |
| `public BufferedInputStream(InputStream is)`   | 把基本流包装成高级流，提高读取数据的性能 |
| `public BufferedOutputStream(OutputStream os)` | 把基本流包装成高级流，提高写出数据的性能 |

#### `BufferedInputStream`



#### `BufferedOutputStream`



### 字符缓冲流

| 方法名称                           | 说明               |
| ---------------------------------- | ------------------ |
| `public BufferedRerader(Reader r)` | 把基本流变成高级流 |
| `public BufferedWriter(Writer r)`  | 把基本流变成高级流 |





#### `BufferedReader`

| 字符缓冲输入流的特有方法   | 说明                                           |
| -------------------------- | ---------------------------------------------- |
| `public String readLine()` | 读取一行数据，如果没有数据可以读了，会返回null |

`readLine`遇到`\r\n`回车换行时才会停止,但是他不会读取\r\n，意味着要自己手动换行，打印读取到的String时用`println`,





#### `BufferedWriter`

| 字符缓冲输出流的特有方法 | 说明         |
| ------------------------ | ------------ |
| `public void newLine()`  | 跨平台的换行 |

不同操作系统中对换行有不同的字符

Mac：\r

Linux:\n

Windows:\r\n





## 转化流

是字节流和字符流之间的桥梁

作用：字节流想要使用字符流中的方法



`InputStreamReader`

`OutputStreamWriter`





## 序列化流 / 对象操作流

### `ObjectOutputStream`

| 构造方法                                      | 说明                 |
| --------------------------------------------- | -------------------- |
| `public ObjectOutputStream(OutputStream out)` | 把基本流包装成高级流 |



| 成员方法                                    | 说明                            |
| ------------------------------------------- | ------------------------------- |
| `public final void writeObject(Object obj)` | 把对象序列化（i写出）到文件中去 |



## 反序列化流 / 对象操作输入流

### `ObjectInputStream`

| 构造方法                                    | 说明               |
| ------------------------------------------- | ------------------ |
| `public ObjectInputStream(InputStream out)` | 把基本流变成高级流 |



| 成员方法                     | 说明                                     |
| ---------------------------- | ---------------------------------------- |
| `public Object readObject()` | 把序列化到本地文件的对象，读取到程序中来 |



### 序列化流和反序列化流的使用细节

- 使用序列化流将对象写到文件时，需要让`javabean`类实现`Serializable`接口，
  否则，会出现`NotSerializableException`异常
- 序列化流写到文件中的数据是不能修改的，一旦修改就无法再次读回来
- 序列化对象后，修改了JavaBean类，再次反序列化会出问题，
  会抛出`InvalidClassException`异常
  解决方案：给JavaBean类添加`serialVersionUID`（序列号、版本号）
- 不想让变量序列化到本地文件就要加一个关键字`transient`（瞬态关键字）修饰
  该关键字标记的成员变量不会参与序列化过程





## 打印流

打印流不能读只能写，把数据写到某个文件中。

打印流一般是指：`PrintStream`、`PrintWrite`两个类



特性1：打印流只能操作文件目的地，不操作数据源

特性2：特有的写出方法可以实现数据原样写出

​			打印 ： 97  		文件中 ： 97

特性3：特有的写出方法可以实现自动刷新，自动换行

​			打印一次数据 = 写出 + 换行 + 刷新



### 字节打印流-------`PrintStream`

| 构造方法                                                     | 说明                             |
| ------------------------------------------------------------ | -------------------------------- |
| `public PrintStream(OutputStream / File / String)`           | 关联字节输出流 / 文件 / 文件路径 |
| `public PrintStream(String fileName, Charset charset)`       | 指定字符编码                     |
| `public PrintStream(OutputStream out, boolean autoFlush)`    | 自动刷新                         |
| `public PrintStream(OutputStream out, boolean autoFlush, String encoding)` | 指定字符编码且自动刷新           |

==注意== : 字节流底层没有缓冲区，开不开自动刷新都一样，都会直接写到文件里



| 成员方法                                            | 说明                                           |
| --------------------------------------------------- | ---------------------------------------------- |
| `public void write(int b)`                          | 常规方法：规则更之前是一样的，将指定的字节写出 |
| `public void println(XXX xxx)`                      | 特有方法：打印任意数据，自动刷新，自动换行     |
| `public void print(XXX xxx)`                        | 特有方法：打印任意数据，不换行                 |
| `public void printf(String format, Object... args)` | 特有方法：带有占位符的打印语句，不换行         |



### 字符打印流------`PrintWriter`

| 构造方法                                                     | 说明                             |
| ------------------------------------------------------------ | -------------------------------- |
| `public PrintWriter(Write / File / String)`                  | 关键字节输出流 / 文件 / 文件路径 |
| `public PrintWriter(String fileName, Charset charset)`       | 指定字符编码                     |
| `public PrintWriter(Write w, boolean autoFlush)`             | 自动刷新                         |
| `public PrintWriter(OutputStream out, boolean autoFlush, Charset charset)` | 指定字符编码和自动刷新           |



| 成员方法                                            | 说明                                           |
| --------------------------------------------------- | ---------------------------------------------- |
| `public void write(...)`                            | 常规方法：规则跟之前的一样，写出字节或者字符串 |
| `public void println(XXX xxx)`                      | 特有方法：打印任意类型的数据并换行             |
| `public void print(XXX xxx)`                        | 特有方法：打印任意类型的数据，不换行           |
| `public void printf(String format, Object... atgs)` | 特有方法：带有占位符的打印语句                 |



### 总结

1. 打印流有几种？各有什么特点？
   - 有字节打印流和字符打印流两种
   - 打印流不操作数据源，只能操作目的地
   - 字节打印流：默认自动刷新，特有的`println`自动换行
   - 字符打印流：自动刷新需要手动开启，特有的`println`自动换行





## 解压缩流 / 压缩流

压缩包里面的每一个文件都是`ZipEntry`对象



解压缩流属于`InputStream`，解压缩本质是把每一个`ZipEntry`按照层级拷贝到本地另外一个文件夹中

```java
public static void main(String[] args) throws IOException {
    //解压缩流
    File src = new File("C:\\develop\\practiceOfFileAndIO\\practice_copyFolder.zip");
    File destination = new File("C:\\develop\\practiceOfFileAndIO");

    //写一个解压缩方法
    unZip(src,destination);

}

private static void unZip(File src, File destination) throws IOException {
    //解压缩本质是把压缩包里的每一个ZipEntry
    ZipInputStream zis = new ZipInputStream(new FileInputStream(src));
    ZipEntry entry;
    while((entry = zis.getNextEntry()) != null) {
        if(entry.isDirectory()) {
            File file = new File(destination,entry.toString());
            System.out.println(file.getName());
            file.mkdirs();
        }else{
            //不是文件夹的话，就直接拷贝文件内容
            FileOutputStream fos = new FileOutputStream(new File(destination,entry.getName()));
            int b = 0;
            while((b = zis.read()) != -1){
                fos.write(b);
            }
            fos.close();
            //关闭zipentry流
            zis.closeEntry();
        }
    }
    zis.close();
}
```

压缩流属于`OutputStream`，压缩的本质就是把每一个（文件 / 文件夹）看成`zipEntry`对象放到压缩包中

 

```java
public static void main(String[] args) throws IOException {
    //关联文件
    File src = new File("C:\\develop\\practiceOfFileAndIO\\copy");
    //压缩包文件路径
    File dest = new File(src + ".zip");
    //创建压缩流
    ZipOutputStream zos = new ZipOutputStream(new FileOutputStream(dest));
    //把文件中的每一个文件和文件夹转化成zipentry
    toZip(src,zos,src.getName());
    //关流
    zos.close();

}
//压缩方法
private static void toZip(File src, ZipOutputStream zos, String name) throws IOException {
    File[] files = src.listFiles();
    for (File file : files) {
        if(file.isFile()){
            //是文件
            ZipEntry ze = new ZipEntry(name + "\\" + file.getName());
            zos.putNextEntry(ze);
            FileInputStream fis = new FileInputStream(file);
            int b = 0;
            while((b = fis.read()) != -1){
                zos.write(b);
            }
            fis.close();
            zos.closeEntry();

        }else{
            //是文件夹
           toZip(file,zos,name + "\\" + file.getName());
        }
    }

}
```





## 字符集



简体中文版windows系统默认使用GBK字符集

GBK字符集完全兼容ASCII字符集

英文：

一个英文占一个字节，二进制第一位是0

汉字：

1. 使用两个字节存储
2. 高位字节二进制一定以一开头，转成十进制之后是一个负数



Unicode也兼容ASCII表

在Unicode中
英文用一个字节表示，二进制第一位是0，转成十进制是正数
中文用三个字节表示，二进制第一位是1，转成十进制是负数

UTF-8不是一种字符集，只是Unicode的一种编码方式




### 为什么会有乱码？

1. 读取数据时未读完整个汉字

   

   

   

   

2. 编码和解码时的方式不统一

如何不产生乱码？

1. 不用字节输入流读取文本文件
2. 编码和解码时使用同一个码表，同一个编码方式



### java中编码和解码的方法

#### 编码的方法

| String类中的方法                            | 说明                 |
| ------------------------------------------- | -------------------- |
| `public byte[] getBytes()`                  | 使用默认方式进行编码 |
| `pblic byte[] getBytes(String charsetName)` | 使用指定方式进行编码 |



#### 解码的方法

| String类中的方法                          | 说明                 |
| ----------------------------------------- | -------------------- |
| `String(byte[] bytes)`                    | 使用默认方法进行解码 |
| `String(byte[] bytes,String charsetName)` | 使用指定方式进行解码 |



编码和解码默认使用的是UTF-编码方式

解码的方法是用在构造方法中的，即往构造方法中放参数

```java
public static void main(String[] args) throws UnsupportedEncodingException {
    //编码
    String str1 = "nb呀";
    //使用默认方式进行编码
    //IDEA中的默认方式是UTF-8
    //而eclipse中的默认方式是GBK
    byte[] bytes1 = str1.getBytes();
    //使用指定方法进行编码
    byte[] bytes2 = str1.getBytes("GBK");
    System.out.println(Arrays.toString(bytes1) + "\r\n" + Arrays.toString(bytes2));
    //[110, 98, -27, -111, -128]
    //[110, 98, -47, -67]

    //解码
    //使用默认方法进行解码
    String str2 = new String(bytes1);
    String str4 = new String(bytes2);
    //使用指定方法进行解码
    String str3   = new String(bytes2,"GBK");
    String str5 = new String(bytes1, "GBK");
    System.out.println(str2);//nb呀
    System.out.println(str4);//nbѽ
    System.out.println(str3);//nb呀
    System.out.println(str5);//nb鍛�

}
```



## Commons-io

commons-io是`apache`开源基金组织提供的一组有关IO操作的开源工具包

作用：提高IO流的开发效率



### commons-io的使用步骤

1. 在项目中创建一个文件夹：lib（以后专门存放第三方的.jar包）
2. 将.jar包复制粘贴到lib文件夹中
3. 右键点击jar包，选择Add as Library -> 点击OK
4. 在类中导包使用



# 多线程



## 线程的基础知识

### 进程和线程的区别

- **线程**：线程是操作系统能够进行运算调度的最小单位，它被包含在进程之中，是进程中的实际运作单位

​			线程简单理解就可以理解为应用软件中相互独立，可以同时运行的功能。

- **进程**：进程是程序的基本执行实体。在Windows操作系统中又分为了多实例进程和单实例进程，多实例在系统中可以打开多份。

  ​	  当一个程序被运行，从磁盘加载这个程序的代码至内存，这时就开启了一个进程。

``` text
在电脑中打开一个软件，比如打开了chrome浏览器或者打开一个文本编辑器都算是一个进程。
多实例就是可以在系统中启动多个相同的进程。比如chrome浏览器，是不是可以同时打开多个呢？可以去试试。
单实例就是只能启动一个进程，比如PC端的微信，只能登录一个账户，登录之后你在点击微信它弹出的是已经登录用户的聊天界面。这就是只能开启一个进程。
```

**对比**

1. 进程是正在运行程序的实例，进程中包括了线程，每个线程执行不同的任务。
2. 不同的进程之间使用的是不同的内存空间，在当前的进程中所有的线程可以共享内存空间
3. 线程更加的轻量，线程上下文切换成本一般要比进程上下文切换低（上下文切换指的是从一个线程切换到另一个线程）。



1. 什么是多线程

   有了多线程，我们就可以让程序同时做多件事情

2. 多线程的作用

   提高效率

3. 多线程的应用场景

   只要是想让多个事情同时运行就需要使用到多线程

   比如：软件中的耗时操作、所有的聊天软件、所有的服务器



### 并发和并行

==并发== ： 在同一时刻，有多个指令在单个`cpu`上交替执行，也可以说是线程轮流使用CPU的做法叫做并发。

==并行==  ： 在同一时刻，有多个指令在多个`cpu`上同时进行



### 线程包括哪些状态，状态之间是如何变化的

这里参考Thread类。

``` java
//在Thread类内部，有个State枚举内部类
public enum State {
    //尚未启动的线程的线程状态
    NEW,
	//可运行线程的线程状态
    RUNNABLE,

    /**
     * 线程阻塞等待监视器锁的线程状态
     * Thread state for a thread blocked waiting for a monitor lock.
     * A thread in the blocked state is waiting for a monitor lock
     * to enter a synchronized block/method or
     * reenter a synchronized block/method after calling
     * {@link Object#wait() Object.wait}.
     */
    BLOCKED,

    /**
     * 等待线程的线程状态
     * Thread state for a waiting thread.
     * A thread is in the waiting state due to calling one of the
     * following methods:
     * <ul>
     *   <li>{@link Object#wait() Object.wait} with no timeout</li>
     *   <li>{@link #join() Thread.join} with no timeout</li>
     *   <li>{@link LockSupport#park() LockSupport.park}</li>
     * </ul>
     *
     * <p>A thread in the waiting state is waiting for another thread to
     * perform a particular action.
     *
     * For example, a thread that has called {@code Object.wait()}
     * on an object is waiting for another thread to call
     * {@code Object.notify()} or {@code Object.notifyAll()} on
     * that object. A thread that has called {@code Thread.join()}
     * is waiting for a specified thread to terminate.
     */
    WAITING,

    /**
     * 具有指定等待时间的等待线程的等待状态
     * Thread state for a waiting thread with a specified waiting time.
     * A thread is in the timed waiting state due to calling one of
     * the following methods with a specified positive waiting time:
     * <ul>
     *   <li>{@link #sleep Thread.sleep}</li>
     *   <li>{@link Object#wait(long) Object.wait} with timeout</li>
     *   <li>{@link #join(long) Thread.join} with timeout</li>
     *   <li>{@link LockSupport#parkNanos LockSupport.parkNanos}</li>
     *   <li>{@link LockSupport#parkUntil LockSupport.parkUntil}</li>
     * </ul>
     */
    TIMED_WAITING,

    /**
     * 已终止线程的线程状态，线程已完成执行。
     * Thread state for a terminated thread.
     * The thread has completed execution.
     */
    TERMINATED;
}
```



![](C:\Users\heban\Desktop\java简历and面试指北\bagu\assets\线程的六种状态.png)

线程一共有六种状态，
NEW，这是新建线程，还没有启动的线程（`Thread.start()`）；
RUNNABLE，可运行的线程；
BLOCK，获取锁失败进入阻塞的线程；
WAITTING，执行了wait() 方法的线程，进入无时间限制的等待状态；
TIME_WAITTING，执行了 sleep(time) 方法的线程，进入了有时间限制的等待；
TERMINATED，执行完所有代码的线程，死亡线程、终止线程；





## 多线程的实现方式



### Thread类

Thread类属于`java.lang`程序包。Thread已经实现了Runnable接口

``` java
public class Thread implements Runnable {
	//代码略
}
```

### 创建线程的方式

#### 继承`Thread`类的方式进行实现

```java
public class myThread extends Thread {

    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println(this.getName() + "Hello World!");
        }
    }
}
```



```java
myThread mt1 = new myThread();
myThread mt2 = new myThread();

mt1.setName("线程一 ：");
mt2.setName("线程二 ：");

mt1.start();
mt2.start();

/*
线程一 ：Hello World!
线程一 ：Hello World!
线程二 ：Hello World!
线程二 ：Hello World!
线程二 ：Hello World!
线程二 ：Hello World!
线程二 ：Hello World!
线程一 ：Hello World!
线程一 ：Hello World!
线程一 ：Hello World!
*/
```



#### 实现Runnable接口的方式进行实现

```java
public class myRun implements Runnable{
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println(Thread.currentThread().getName() + " hello world！");
        }
    }
}
```



```java
//创建myRun对象
//表示多线程需要执行的任务
myRun r1 = new myRun();
//创建线程对象
Thread t1 = new Thread(r1);
Thread t2 = new Thread(r1);
//开启线程
t1.start();
t2.start();
```





#### 利用`Callable`接口和`Future`接口方式进行实现

特点：可以获取到多线程运行的结果

```java
public class mycallable implements Callable<Integer> {
    //求1~10的和
    @Override
    public Integer call() throws Exception {
        int sum = 0;
        for (int i = 1; i <= 10; i++) {
            sum += i;
        }

        return sum;
    }
}
```



```java
/*

重写call（是有返回值的，表示多线程运行的结果）

创建一个MyCallable实现Callable（表示多线程要执行的任务）
创建FutureTask对象（作用 管理多线程运行的结果）
创建Thread类对象， 并启动（表示线程）

 */

//创建一个MyCallable实现Callable（表示多线程要执行的任务）
mycallable mc = new mycallable();
//创建FutureTask对象（作用 管理多线程运行的结果）
FutureTask ft = new FutureTask(mc);
//创建Thread类对象， 并启动（表示线程）
new Thread(ft).start();

System.out.println(ft.get());
//如果是有多个线程都有各自的结果，则应该创建多个FutureTask对象来管理返回结果
```



#### 线程池创建线程

线程池知识可以看后面线程池小节。



#### 对比

|                    | 优点                                         | 缺点                                         |
| ------------------ | -------------------------------------------- | -------------------------------------------- |
| 继承`Thread`类     | 编程比较简单，可以直接使用`Thread`类中的方法 | 可以拓展性差，不能再继承其他的类             |
| 实现`Runnable`接口 | 拓展性强，实现该接口的同时还可以继承其他的类 | 编程相对复杂，不能直接使用`Thread`类中的方法 |
| 实现`Callable`接口 | 与`Runnable`接口优点一样                     | 与`Runnable`接口缺点一样                     |



##### `Runnable`和`Callable`的区别

- runnable中的run方法没有返回值，但是Callable的call方法有返回值，而且是泛型，和`Future`、`FutureTask`配合可以用来获取异步执行的结果。
- call方法可以抛出异常，但是run方法不能向上抛出异常，只能内部消化，不能向上抛出。



##### run和start方法

###### `run` 方法

1. **定义**：`run` 方法是 `Runnable` 接口中的一个方法，它定义了线程要执行的代码。
2. **作用**：当你创建一个实现了 `Runnable` 接口的类的实例时，你需要在 `run` 方法中编写你希望线程执行的代码。
3. **调用**：`run` 方法可以通过直接调用或者通过 `Thread` 类的 `start` 方法间接调用。

###### `start` 方法

1. **定义**：`start` 方法是 `Thread` 类中的一个方法，用于启动线程。
2. **作用**：调用 `start` 方法会启动一个新的线程，使得 `run` 方法在新的线程中执行。
3. **调用**：`start` 方法只能被调用一次，一旦线程启动，再次调用 `start` 方法会导致 `IllegalThreadStateException`。

###### 区别

1. **执行环境**：
   - `run` 方法可以在任何地方调用，它只是普通的方法调用，不会启动新的线程，`run` 方法的代码会在调用它的那个线程中执行。
   - `start` 方法必须在 `Thread` 类的实例上调用，它会启动一个新的线程，使得 `run` 方法在新的线程中执行。
2. **线程状态**：
   - 当你直接调用 `run` 方法时，线程状态不会发生变化，它仍然是在调用它的线程中执行。
   - 当你调用 `start` 方法时，线程状态会从 `NEW` 变为 `RUNNABLE`，表示线程已经准备好开始执行。
3. **线程调度**：
   <!--线程调度是操作系统或运行时环境（如 Java 虚拟机）管理线程执行的过程。它决定了哪个线程何时获得 CPU 时间来执行。线程调度的目标是合理地分配 CPU 资源，以提高系统的整体性能和响应性。-->
   - 直接调用 `run` 方法不会进行线程调度，`run` 方法的执行不会受到线程调度器的控制。
   - 调用 `start` 方法后，线程的执行会受到线程调度器的控制，线程调度器会决定何时以及如何分配 CPU 时间给线程。



> 测试run方法和start方法是否真的一个是不开启新的线程，一个是开启新的线程
>
> ``` java
> static class myRunnable implements Runnable{
> @Override
> public void run() {
>   System.out.println(Thread.currentThread().getName());
> }
> }
> 
> @Test
> public void testThread(){
> System.out.println(Thread.currentThread().getName());
> 
> new Thread(){
>   @Override
>   public void run() {
>       System.out.println(Thread.currentThread().getName());
>   }
> }.start();
> 
> Runnable myRunnable = new myRunnable();
> myRunnable.run();
> } 
> /*
> 执行结果:
> main
> Thread-0
> main
> */
> ```
>
> 



### 如何保证线程之间按顺序执行

可以使用`join()`方法，`线程1.join()`表示当前线程会等待线程1执行完后才开始执行。这个join方法下节有讲。

这样就可以让线程之间有顺序的执行了。



### 如何停止一个正在运行的线程

有三种方法：

- 使用退出标志，使线程正常退出，也就是当run方法完成后线程退出。
- 使用`Thread`类中的`stop`方法强行终止（不推荐，方法已经作废）
- 使用`interrupt`方法中断线程
  1. 打断阻塞的线程（sleep、wait、join）的线程，线程就会抛出`InterruptedException`异常
  2. 打断正常的线程，可以根据打断的状态来标记是否退出线程







## 常见的成员方法

| 方法名称                           | 说明                                                         |
| ---------------------------------- | ------------------------------------------------------------ |
| `String getName()`                 | 返回此线程的名称                                             |
| `void setName(String name)`        | 设置线程的名称（构造方法也可以设置名称，子类的话需要自己写调用`super()`的构造方法） |
| `static Thread currentThread()`    | 获取当前线程的对象<br/>细节： 当JVM虚拟机启动之后会自动启动多条线程，其中有一条线程就叫做main线程<br/>它的作用就是取调用main方法，并执行里面的代码<br/>在以前，我们写的所有代码，其实都是运行在main线程中 |
| `static void sleep(long time)`     | 让线程休眠指定的时间，单位为毫秒<br/>哪条线程执行到这个方法，那么哪条线程就会在这里停留相对应的时间<br/>参数就表示睡眠的时间<br/>当时间到了之后，线程会自动醒过来，继续执行下面的其他代码 |
| `setPriority(int newPriority)`     | 设置线程的优先级，优先级最小是1，最大是10，<br/>默认是取中间的5，优先级越大，抢占到`cpu`的概率也就越大 |
| `final int getPriority()`          | 获取线程的优先级                                             |
| `final void setDaemon(boolean on)` | 设置为守护线程                                               |
| `public static void yield()`       | 出让线程 / 礼让线程                                          |
| `public static void join()`        | 插入线程 / 插队线程                                          |



### 优先级

优先级越高，代表抢占`cpu`概率越大，当优先级为10时表示抢占`cpu`概率最大，而不是百分百抢到`cpu`。



### 守护线程

当其他非守护线程执行完毕后，守护线程也会陆续结束，注意是陆续，而不是马上，在非守护线程执行完毕之后，守护线程接下来执行多少次而结束是不固定的。



### 出让线程 / 礼让线程

当前抢占到`cpu`的线程执行完成后，会释放对`cpu`的占用，让各线程重新抢占`cpu`



### 插入线程 / 插队线程

```java
t.join();
//表示t线程插入到当前线程前面
```



### `notify()`和`notifyAll()`有什么区别

- `notifyAll()`是唤醒所有`wait`的线程
- `notify()`是随机唤醒一个`wait`中的线程



### `wait()`方法和`sleep()`方法有什么不同

#### 共同点

  `wait()`、`wait(long)`和`sleep(long)`的效果都是让调用方法的线程暂时放弃CPU的使用权，进入阻塞状态。

#### 不同点

  1. 方法归属不同

     `sleep(long)`方法是`Thread`类的静态方法

     `wait()`和`wait(long)`方法都是Object的成员方法，每个对象都有

  2. 醒来时机不同

     执行`sleep(long)`和`wait(long)`的线程都会在等待响应毫秒后醒来

     `wait(long)`和`wait()`方法可以使用`notify()`方法唤醒，`wait()`方法如果不唤醒就一直等下去

     三个方法都可以被打断唤醒

  3. **锁的特性不同（重点）**

     `wait()`方法的调用必须先获取`wait`对象的锁，而`sleep`则无限制

     ```java
     sychronized(LOCK){
     	LOCK.wait();
     }
     ```

     `wait()`方法执行后会释放对象锁，允许其他线程获取该对象锁（我放弃cpu，但是你们还可以用）

     而`sleep`如果在synchronized代码块中执行，并不会释放对象锁（我放弃cpu，但是你们也不能用）

     

     


### `wait` 方法和 `await` 方法的区别

这两种方法都与线程或异步任务的协调有关，但它们用于不同的场景，并且行为和语法都不相同。

#### **1. `wait()` 方法**

##### **定义与场景**

- **所属**：`java.lang.Object` 类。
- **用途**：用于线程间的通信，通常与 `notify()` 或 `notifyAll()` 方法一起使用。
- **场景**：在多线程程序中，一个线程等待某些条件满足，而另一个线程通知它继续执行。

##### **关键特点**

- 必须在同步块（`synchronized`）或同步方法中调用，否则会抛出 `IllegalMonitorStateException`。
- 调用 `wait()` 的线程会释放锁并进入 **等待状态**，直到另一个线程调用 `notify()` 或 `notifyAll()` 唤醒它。
- 属于阻塞操作，调用后线程会停止运行，直到被唤醒。

##### **语法**

```java
synchronized(lock) {
    lock.wait();// 释放锁并进入等待状态
}
```

　　

##### **示例**

```java
class WaitNotifyExample {
    private static final Object lock = new Object();

    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            synchronized (lock) {
                try {
                    System.out.println("Thread 1 is waiting...");
                    lock.wait();
                    System.out.println("Thread 1 is resumed!");
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        Thread t2 = new Thread(() -> {
            synchronized (lock) {
                System.out.println("Thread 2 is notifying...");
                lock.notify();
            }
        });

        t1.start();
        t2.start();
    }
}
```

　　

```java
//输出
Thread 1 is waiting...
Thread 2 is notifying...
Thread 1 is resumed!
```

​	

#### **2. `await()` 方法**

##### **定义与场景**

```java
所属：java.util.concurrent.locks.Condition 接口。
 
用途：用于高级线程协调，通常结合 ReentrantLock 使用。
 
场景：细粒度控制线程的等待和唤醒操作，在并发编程中提供更灵活的机制。
 
关键特点
必须在锁对象（如 ReentrantLock）的条件中使用，不能在普通的同步块中使用。
 
与 wait() 类似，调用线程会释放锁并进入等待状态，直到被其他线程通过 signal() 或 signalAll() 唤醒。
 
提供更好的线程通信控制，可以使用多个条件（Condition），而不像 wait() 只能针对一个对象锁。
 
语法
ReentrantLock lock = new ReentrantLock();
Condition condition = lock.newCondition();
​
lock.lock();
try {
    condition.await(); // 释放锁并进入等待状态
} finally {
    lock.unlock();
}
　　
 
示例
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.ReentrantLock;
​
class AwaitSignalExample {
    private static final ReentrantLock lock = new ReentrantLock();
    private static final Condition condition = lock.newCondition();
​
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            lock.lock();
            try {
                System.out.println("Thread 1 is waiting...");
                condition.await();
                System.out.println("Thread 1 is resumed!");
            } catch (InterruptedException e) {
                e.printStackTrace();
            } finally {
                lock.unlock();
            }
        });
​
        Thread t2 = new Thread(() -> {
            lock.lock();
            try {
                System.out.println("Thread 2 is signaling...");
                condition.signal();
            } finally {
                lock.unlock();
            }
        });
​
        t1.start();
        t2.start();
    }
}
```

　　

##### **输出**

```java
Thread 1 is waiting...
Thread 2 is signaling...
Thread 1 is resumed!
```



#### 对比总结

| 特性                 | **`wait()`**                           | **`await()`**                                  |
| -------------------- | -------------------------------------- | ---------------------------------------------- |
| **所属类**           | `java.lang.Object`                     | `java.util.concurrent.locks.Condition`         |
| **使用锁类型**       | Java 内置锁（`synchronized`）          | 显式锁（`ReentrantLock`）                      |
| **等待/唤醒方法**    | `wait() / notify() / notifyAll()`      | `await() / signal() / signalAll()`             |
| **是否释放锁**       | 释放锁，等待被通知                     | 释放锁，等待被通知                             |
| **灵活性**           | 只能使用一个对象锁，功能较为简单       | 可以为不同条件创建多个 `Condition`，功能更强大 |
| **线程安全控制粒度** | 粒度较粗                               | 粒度更细                                       |
| **是否支持中断**     | 可以通过 `InterruptedException` 被中断 | 同样支持 `InterruptedException`                |



#### 选择建议

- **`wait()`**：
  - 如果是传统的 `synchronized` 代码块，使用 `wait()` 即可。
  - 适合简单的线程间协调。
- **`await()`**：
  - 如果需要更复杂的线程控制（如多个条件或高级同步机制），推荐使用 `await()` 和 `ReentrantLock`。
  - 更适合高并发场景。



## 同步代码块

把操作共享数据的代码锁起来

格式：

```java
synchronized(锁对象){
	//操作共享数据的代码
}
//特点一：锁默认打开，有一个线程进去了，锁自动关闭
//特点二：里面的所有代码执行完毕之后，线程出来，锁自动打开
```



### **`synchronized`关键字的底层原理**

- `synchronized(对象锁)`采用互斥的方式让同一时刻至多只有一个线程可以持有【对象锁】，其他的线程想要获取【对象锁】时就会进入阻塞状态。

- synchronized底层是使用了Monitor监视器的，Monitor由JVM提供，c++实现的。**线程获取锁需要使用对象锁关联monitor**

  ```tex
  Monitor结构:
  WaitList // 存放调用了wait方法的线程，处于Wating状态的线程。
  EntryList //存放没有抢到锁的线程，处于Blocking状态的线程，这里面的线程并不是按排序来获得锁的，是看谁先抢到锁对象，并不是先来后到。
  Owner //存储当前获取锁的线程，只有一个线程可以获取。
  ```

  `synchronized`编译后上锁使用的是`monitorenter`，释放锁使用的是`monitorexit`,并且编译后的代码中会有两次释放锁，第一次是正常情况下释放（补充：编译后的代码中隐式的使用了try{……}catch{……}finally{……}包住，防止抛出异常后锁没有释放），第二次是释放是保障抛出异常后还是可以正常释放锁。



#### 锁升级

Monitor实现的锁属于重量级锁，里面会涉及到用户态和内核态的切换、进程的上下文切换，成本较高，性能比较低。

在JDK1.6引入了两种新型锁机制：**偏向锁和轻量级锁**，这两个锁的引入是为了解决在竞争所强度低的情况下传统锁机制带来的性能开销问题。



##### Monitor重量级锁

上面说到了锁对象关联Monitor，但这是怎么关联上的呢？这就需要了解下java对象的内存结构。

![](C:\Users\heban\Desktop\java简历and面试指北\bagu\assets\java对象内存结构.png)

> HotSpot是一种实现虚拟机的技术。现在大多数的虚拟机都是HotSpot虚拟机。
>
> 重点需要学习MarkWord
>
> ![](C:\Users\heban\Desktop\java简历and面试指北\bagu\assets\java对象内存结构中的MackWord字段结构.png)
>
> 看完这张图片后，就可以知道了，**锁对象是通过 `MarkWord` 中的`ptr_to_heavyweight_monitor`来指定monitor地址的。**这样就关联到了monitor。

**每个java对象都可以关联一个Monitor对象，如果使用synchronized给对象上锁（重量级）之后，该对象头的`MarkWord`中就会被设置指向Monitor对象的指针。**





##### 轻量级锁

在很多的情况下，在Java程序运行时，同步块中的代码都是不存在竞争的，不同的线程交替的执行同步块中的代码。这种情况下，用重量级锁是没必要的。因此JVM引入了轻量级锁的概念。

###### 加锁流程

1. 在线程栈中创建一个Lock Record，将其obj字段指向锁对象。
2. 通过CAS指令将Lock Record的地址存储在对象头的mark word中，如果对象处于无锁状态则修改成功，代表该线程获得了轻量级锁。
3. 如果是当前线程已经持有该锁了，代表这是一次锁重入。设置Lock Record第一部分为null，起到了一个重入计数器的作用。
4. 如果CAS修改失败，说明发生了竞争，需要膨胀为重量级锁。



###### 解锁过程

1. 遍历线程栈,找到所有obj字段等于当前锁对象的Lock Record。
2. 如果Lock Record的Mark Word为null，代表这是一次重入，将obj设置为null后continue。
3. 如果Lock Record的 Mark Word不为null，则利用CAS指令将对象头的mark word恢复成为无锁状态。如果失败则膨胀为重量级锁。



##### 偏向锁

轻量级锁在没有竞争时（就自己这个线程），每次重入仍然需要执行 CAS 操作。Java 6 中引入了偏向锁来做进一步优化：只有第一次使用 CAS 将线程 ID 设置到对象的 Mark Word 头，之后发现这个线程 ID 是自己的就表示没有竞争，不用重新 CAS。以后只要不发生竞争，这个对象就归该线程所有





##### Monitor实现的锁属于重量级锁，你了解过锁升级吗？

Java中的synchronized有偏向锁、轻量级锁、重量级锁三种形式，分别对应了锁只被一个线程持有、不同线程交替持有锁、多线程竞争锁三种情况。

**一旦锁发生了竞争，都会升级为重量级锁**





### 同步方法 - synchronized

就是把**`synchronized`关键字**加到方法上,synchronized关键字可以对对象加互斥锁

格式：

```java
修饰符 synchronized 返回值类型 方法名(方法参数){
	//代码
}

//特点一：同步方法是锁住方法里面所有的代码
//特点二：锁对象不能自己指定
//当方法是静态的，则锁对象是当前类的字节码文件对象
//当方法是非静态的，则锁对象是this(当前方法的调用者)
```



### lock锁

同步代码块和同步方法我们不知道锁在哪里上了锁，在哪里释放了锁，为了更清晰的表达如何加锁，如何释放锁

JDK5以后提供了一个新的锁对象`Lock`



`Lock`中提供了获得锁和释放锁的方法

```java
void lock()//获得锁（上锁）
void unlock()//释放锁
```



==注意== ：  `Lock`是接口不能直接实例化，这里采用它的实现类`ReentrantLock`来实例化

`ReentrantLock`的构造方法

```java
ReentrantLock()//创建一个ReentrantLock的实例
    
//Lock lock = new ReentrantLock();
```





### `synchronized`和`Lock`有什么区别

- 语法层面

`synchronized`是关键字，源码在jvm中，由c++实现

Lock是接口，源码由jdk提供，由java实现

使用 synchronized 时，退出同步代码块锁会自动释放，而使用 Lock 锁时，需要手动调用 unlock 方法释放锁。

- 功能层面

二者均属于悲观锁、都具备基本的互斥、同步、锁重入功能

Lock 提供了许多 synchronized 不具备的功能，例如公平锁、可打断、可超时、多条件变量

Lock 有适合不同场景的实现，如 ReentrantLock， ReentrantReadWriteLock(读写锁)

- 性能层面

在没有竞争时，synchronized 做了很多优化，如偏向锁、轻量级锁，性能不赖

在竞争激烈时，Lock 的实现通常会提供更好的性能





## `CAS`

CAS的全称是：Compare And Swap（比较再交换），它体现的一种乐观锁的思想，在无锁情况下保证线程操作共享数据的原子性。

CAS使用到的地方很多：AQS框架、`AtomicXXX`类

在操作共享数据的时候使用自旋锁，效率上更高一点。

CAS 底层依赖于一个 Unsafe 类来直接调用操作系统底层的 CAS 指令



由此可以引出：

### 乐观锁和悲观锁

- CAS  是基于乐观锁的思想：最乐观的估计，不怕别的线程来修改共享变量，就算改了也没关系，我吃亏点再重试呗。

- synchronized  是基于悲观锁的思想：最悲观的估计，得防着其它线程来修改共享变量，我上了锁你们都别想改，我改完了解开锁，你们才有机会。



## 关键字`volatile`

一旦一个共享变量（类的成员变量、类的静态成员变量）被volatile修饰之后，那么就具备了两层语义：

- **保证线程间的可见性**：用 volatile 修饰共享变量，能够防止编译器等优化发生，让一个线程对共享变量的修改对另一个线程可见

  ```java
  //
  public boolean flag = false;
  
  new Thread(() -> {
      int i = 0;
      while(!flag){
          i++;
      }
      sout(i);
  },"t1").start();
  //t1线程开始运行后，就算别的线程把flag修改为true之后，t1线程还是不会停止循环，为什么会这样呢？
  //主要是因为在JVM虚拟机中有一个JIT（即时编译器）给代码做了优化。
  while(!flag){        优化			while(true){
      i++;		   ------->   		i++;
  }								}
  ```

  ​	怎么解决即时编译器的带来的影响呢？

  1. 解决方案一：在程序运行的时候加入vm参数-Xint表示禁用即时编译器，不推荐，得不偿失（其他程序还要使用）

  2. 解决方案二：在修饰stop变量的时候加上volatile,当前告诉 jit，不要对 volatile 修饰的变量做优化

     ```java
     public volatile boolean flag = false;
     ```

     

  

- **禁止进行指令重排序**：用 volatile 修饰共享变量会在读、写共享变量时加入不同的屏障，阻止其他读写操作越过屏障，从而达到阻止重排序的效果

  ​				    给变量 y 用`volatile`修饰
  
  ![volatile禁止指令重排序图](C:\Users\heban\Desktop\java简历and面试指北\bagu\assets\volatile禁止指令重排序图.png)

写屏障就是保证被修饰的变量是在最后执行的，但是不能保证自己会比自己后面的代码先执行。

读屏障就是保证被修饰的代码会比自己后面的代码先执行。

### **volatile使用技巧：**

- 写变量让volatile修饰的变量的在代码最后位置
- 读变量让volatile修饰的变量的在代码最开始位置





## 线程池



### 主要核心原理

1. 创建一个池子，池子中是空的
2. 提交任务时，池子会创建新的线程对象，任务执行完毕，线程归还给池子，下回提交任务时，不需要创建新的线程，直接复用已有的线程即可
3. 但是如果提交任务时，池子中没有空闲的线程，也无法创建新的线程，任务就会排队等待





### 线程池代码实现

`Executors` : 线程池的工具类，通过调用方法返回不同类型的线程池对象。

| 方法名称                                                     | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `public static ExecutorService newCachedThreadPool()`        | 创建一个没有上限的线程池,(并不是真正意义上的无上限，上限是int的最大值) |
| `public static ExecutorService newFixedThreadPool(int nThreads)` | 创建一个有上限的线程池                                       |



```java
//获取线程池
ExecutorService executorService = Executors.newCachedThreadPool();
//提交一个任务
executorService.submit(new myRun());
//销毁线程池，但是一般不会自己主动销毁线程池
executorService.shutdown();
```





### `ThreadLocal`

 **`ThreadLocal`本质上就是一个大Map集合Map<Thread,Object>**

`ThreadLocal`理解 [](https://www.bilibili.com/video/BV1Z3411C7NZ?p=74&vd_source=df4529d9e18c20a7759796e70b88ca1c)



>想学习`ThreadLocal`，就需要先了解下`ThreadLocal`的结构

``` java
//ThreadLocal 类
public class ThreadLocal<T> {
    //ThreadLocalMap是ThreadLocal提供的静态内部类
    static class ThreadLocalMap {
		//成员变量 --- Entry --- ThreadLocalMap又提供了一个静态内部类
        static class Entry extends WeakReference<ThreadLocal<?>> {
            /** The value associated with this ThreadLocal. */
            Object value;

            Entry(ThreadLocal<?> k, Object v) {
                super(k);
                value = v;
            }
        }
        //成员变量 --- Entry[] --- 真正储存数据的地方
        private Entry[] table;
        
        //成员方法 --- set --- 向外暴露的API，就是ThreadLocal常用的存储数据的方法set
        public void set(T value) {
            //获取使用ThreadLocal的线程
            Thread t = Thread.currentThread();
            
            ThreadLocalMap map = getMap(t);
            if (map != null) {
                map.set(this, value);
            } else {
                createMap(t, value);
            }
    	}
        
        /**
        * @param 获取哪个线程的ThreadLocalMap
        * @return 返回指定线程的ThreadLocalMap
        */
        ThreadLocalMap getMap(Thread t) {
        	return t.threadLocals;
        }
        
        /**
        * 成员方法 --- set--- 这个方法是私有的，被上面公共set方法调用，内部实现过程隐藏起来
        * @param key 主键是使用的ThreadLocal
        * @param value 需要存储的数据
        */
        private void set(ThreadLocal<?> key, Object value) {

            // We don't use a fast path as with get() because it is at
            // least as common to use set() to create new entries as
            // it is to replace existing ones, in which case, a fast
            // path would fail more often than not.
			
            Entry[] tab = table;
            int len = tab.length;
            int i = key.threadLocalHashCode & (len-1);//计算key值在散列表中的位置

            for (Entry e = tab[i];
                 e != null;
                 e = tab[i = nextIndex(i, len)]) {
                if (e.refersTo(key)) {
                    e.value = value;
                    return;
                }

                if (e.refersTo(null)) {
                    replaceStaleEntry(key, value, i);
                    return;
                }
            }

            tab[i] = new Entry(key, value);
            int sz = ++size;
            if (!cleanSomeSlots(i, sz) && sz >= threshold)
                rehash();
        }

}
```



``` java
//Thread 类
public class Thread implements Runnable {
    
    /**
    * 成员变量
   	* 类型是ThreadLocal的静态内部类
    */
    ThreadLocal.ThreadLocalMap threadLocals = null;
    
}
```



总结：`ThreadLocal`是不是把数据存储在这个线程池里面，而是把数据存储在调用这个线程池的线程中，真正存储的位置在线程池的`ThreadLocalMap`对象中。

看完底层源码，可以知道，在`ThreadLocal`的存储规则中，key是使用的`ThreadLocal`，也就是说，每个线程只能在一个`ThreadLocal`中存储一个数据。





# 网络编程

网络编程 ： 计算计跟计算机之间通过网络进行数据传输



常见的软件架构 : CS / BS 



## 网络编程的三要素 

###  IP

上网设备在网络中的地址，是唯一的标识。



#### IPv4

目前主流方案，最多2^32次方个IP，目前已经用完了

IPv4的地址分类形式：公网地址（万维网使用）和私有地址（局域网使用）

特殊IP地址，127.0.0.1，也可以是localhost，是回送地址也称本地回环地址，也称本机IP，永远只会寻找当前所在本机





#### IPv6

为了解决IPv4不够用而出现的，最多有2^128次方个IP







### 端口号

应用程序在设备中的唯一标识。

由两个字节表示的整数，取值范围 ： 0 ~ 65535

一个端口号只能被一个应用程序使用



### 协议

数据在网络中传输的规则，常见的规则有UDP、TCP、http、https、ftp



#### UDP协议

- 用户数据报协议 (User Datagram Protocol)

- UDP是**面向无连接**通信协议

  速度快，有大小限制一次最多发送64K，数据不安全，已丢失数据



##### 发送数据

1. 创建发送端的`DatagramSocket`对象

   ```java
   //细节：
   //会进行绑定端口操作：以后我们就会通过这个端口往外发送数据
   //空参：所有可用的端口中随机一个进行使用
   //有参：指定端口号进行绑定
   ```

2. 数据打包(`DatagramPacket`)

3. 发送数据

4. 释放资源



##### 接收数据

1. 创建接收端的`DatagramSocket`对象

   ```java
   //细节
   //在接收时一定要绑定端口，而且绑定的端口一定要和发送的端口保持一致
   ```

2. 接收打包好的数据

   ```java
   ds.receive(dp);
   //该方法是阻塞的，程序执行到这一步会一直死等，等待发送端发送数据
   ```

3. 解析数据包

4. 释放资源



##### 三种通信方式

1. 单播
2. 组播
3. 广播





#### TCP协议

- 传输控制协议（Transmission Control Protocol）

- TCP协议是**面向连接**的通信协议

  速度慢，没有大小限制，数据安全



# 反射

## 什么是反射？

反射是在运行过程中，对于任意一个类，都可以获取它的全部属性和方法信息；对于任意一个对象，都可以调用它的任意一个属性和方法，这种动态获取信息以及动态调用对象方法的功能就叫做Java语言的反射机制。



反射的作用

1. 获取任意一个类中的所有信息
2. 结合配置文件动态创建对象



## 反射机制的优缺点是什么？

**优点**：

- 能够在运行时动态的获取信息以及动态调用对象方法（动态获取类的实例），提高灵活度；
- 可与动态编译结合，``Class.forName("com.mysql.jdbc.Driver.class");``，加载MySQL驱动；

**缺点**：

-  使用反射性能较低，需要解析字节码，将内存中的对象进行解析

缺点的解决方法：

+ 通过``setAccessible(true)``关闭JDK的安全检查来提升反射速度；

- 多次创建一个类的实例时，有缓存会快很多；

- ``ReflflectASM``工具类，通过字节码生成的方式加快反射速度









## 认识反射中的一些类



### `Type`

`Type` 是一个接口，它是 Java 编程语言中所有类型的通用超级接口。`Type` 接口定义了 Java 中所有类型的结构，包括原始类型（`Class`）、参数化类型（`ParameterizedType`）、数组类型（）、类型变量（`TypeVariable`）和基本类型（`Class`）。



根据例子来理解

对象类

```java
package com.atguigu.reflect;

public class User {
    private String name;
    private int age;
    
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
    
    public void doSome(){
        System.out.println("public void doSome()执行了！");
    }
    
    public void doSome(String name){
        System.out.println("public void doSome(String name)执行了！");
    }
    
    public void doSome(String name,int age){
        System.out.println("public void doSome(String name, int age)执行了！");
    }
    
}
```



```java
package com.atguigu.reflect;

import org.junit.jupiter.api.Test;

import java.lang.reflect.Constructor;
import java.lang.reflect.Method;

public class reflectTest {
    @Test
    public void test() throws Exception{
        /**
         * 获取类，有三种方式
         * Class.forName("全名");
         * 类名.class;
         * 对象.getClass();
         */

        Class<?> clazz = Class.forName("com.atguigu.reflect.User");

        /**
         * 获取对象方法有两个方法
         * 第一个：
         *       clazz.getDeclaredMethod(String methodName,Class<?>... methodParameterType);
         *       返回类型是指定的方法（一个方法）
         *       第一个参数是指定方法的名字
         *       后面的参数就是指明方法中的参数的类
         *       -->为什么会需要指明参数的类，因为在一个类中可以有方法重载，方法名是一样的，只有方法的参数不一样
         *       比如：
         *          Method doSomeMethod = clazz.getDeclaredMethod("doSome",String.class,int.class);
         *          这个返回的就是public String doSome(String name,int age)这个方法
         *          Method doSomeMethod = clazz.getDeclaredMethod("doSome",String.class);
         *          这个返回的就是public String doSome(String name)
         *          Method doSomeMethod = clazz.getDeclaredMethod("doSome");
         *          这个返回的就是public void doSome()
         *
         * 第二个：
         *       clazz.getDeclaredMethods();
         *       返回类型是Method[]（方法数组）
         *       第二个方法没有参数，返回的是对象中的全部方法
         *
         */
        Method doSomeMethod = clazz.getDeclaredMethod("doSome",String.class,int.class);

        /**
         * 创建一个对象
         * 可以直接用过时的方法,创建一个对象
         * Class.newInstance() 只能够调用无参的构造函数，即默认的构造函数；
         * Object obj = clazz.newInstance();
         *
         * 也可以获取构造器对象来创建一个对象
         * Constructor.newInstance()
         * 例子
         *         Constructor<?> constructor = clazz.getConstructor();
         *         Object obj = constructor.newInstance(Object...initargs);
         *         带有一个可变参数，用于创建一个有参构造函数的实例。这里的 initargs 是一个对象数组，包含了传递给构造函数的参数。
         *         不带参数就是调用无参构造方法
         *
         */
        Constructor<?> constructor = clazz.getConstructor();
        Object obj = constructor.newInstance();

        /**
         * 调用方法
         * 调用哪个对象的哪个方法，传什么参数，返回什么类型
         * Method.invoke(Object object,Object...args);
         * object对象调用Method方法，传入args可变参数，返回类型与invoke方法的返回类型一致。
         * returnResult就是返回的数据
         *
         * 注意：如果是私有方法，就是用private修饰的方法，需要使用setAccessible方法设置为可以访问的，不然会报错。
         */
        doSomeMethod.setAccessible(true);
        Object returnResult = doSomeMethod.invoke(obj, "张三", 250);

        System.out.println(returnResult);
		
        /**
         * 获取成员变量
         * Field declaredField = clazz.getDeclaredField(String name);
         * 根据属性名获取指定的成员变量
         * Field[] declaredFields = clazz.getDeclaredFields();
         * 获取对象类的所有成员变量，对成员变量操作获取具体信息
         * getName()获取成员变量的属性名
         * getType()获取成员变量的属性类型
         */

        Field declaredField1 = clazz.getDeclaredField("name");
        System.out.println(declaredField1.getName());//name

        Field[] declaredFields = clazz.getDeclaredFields();
        for (Field declaredField : declaredFields) {
            System.out.println(declaredField.getName() + " " + declaredField.getType());
        }
        //name class java.lang.String
        //age int
        
    }
}
/*
public void doSome(String name, int age)执行了！
张三250

*/

```



## 如何获取反射中的class对象？

1. ``Class.forName(“类的路径”)``；当你知道该类的全路径名时，你可以使用该方法获取 Class
    类对象。

  ```java
  Class clz = Class.forName("java.lang.String");
  ```

2. 类名.class。这种方法只适合在编译前就知道操作的 Class。

   ``` java
   Class clz = String.class;
   ```

3. 对象名.getClass()。

   ``` java
   String str = new String("abc");
   Class clz = str.getClass();
   ```

4. 如果是基本类型的包装类，可以调用包装类的Type属性来获得该包装类的Class对象。

   ``` java
   //基本类型的包装类  int 的包装类就是 Integer
   Class clz = Integer.Type;
   
   //Type 是类中的一个属性
   public static final Class<Integer>  TYPE = (Class<Integer>) Class.getPrimitiveClass("int");
       
   ```






## 反射机制的原理是什么？





## 获取方法

```java
//get 获取
//Constructor 构造方法
//Field 成员变量
//Method 方法
//set 设置
//Parameter 参数
//Modifiers 修饰符
//Declared 私有的
```





## 利用反射获取的泛型信息



### 获取类上的泛型信息



```java
//这里object表示的是我们自己定义的一个类，也就是需要从object类中获取泛型信息
//第一步
Type genericSuperclass = object.class.getGenericSuperclass();
/*方法解释：
	getGenericSuperclass()：返回该类的直接父类的泛型类型信息。如果父类是泛型化的，返回的是一个 ParameterizedType 对象；否则返回 null。
	如果object类定义为：public class object<T> extends ArrayList<T> {} ，getGenericSuperclass() 会返回 ArrayList<T> 的泛型类型信息。
	如果object类定义为：public class object<T>{} ，getGenericSuperclass()方法就会返回null。
*/

//第二步
ParameterizedType parameterizedType = (ParameterizedType) genericSuperclass;
/*
	ParameterizedType：表示参数化类型（如 ArrayList<T>）。它是一个接口，继承自 Type 接口。
	ParameterizedType 提供了以下方法：
		getRawType()：返回原始类型（如 ArrayList.class）。
		getActualTypeArguments()：返回实际的类型参数（如 [T]）。
		getOwnerType()：返回所属的类型（如果有的话）。
*/

//第三步
Type[] actualTypeArguments = parameterizedType.getActualTypeArguments();
/*
	获取类型上所有的泛型类型
*/

//第四步
System.out.println(actualTypeArguments[0]); // 输出 T
```



例子：

``` java
// 父类：带泛型
class Parent<T> {
}

// 子类：继承父类，并指定泛型为 String
class User extends Parent<String> {
}
```



``` java
// 1. 获取 User 类的【带泛型的父类】
// 得到：Parent<String>
Type genericSuperclass = User.class.getGenericSuperclass();

// 2. 强转成“参数化类型”（就是带 <> 泛型的类型）
ParameterizedType parameterizedType = (ParameterizedType) genericSuperclass;

// 3. 获取泛型里的【实际类型参数】
// 也就是 <> 里面写的东西
Type[] actualTypeArguments = parameterizedType.getActualTypeArguments();

// 4. 遍历输出
// 这里会输出：class java.lang.String
for (Type actualTypeArgument : actualTypeArguments) {
    System.out.println(actualTypeArgument);
}
```





# 原理



## 基础



### 注解



**能讲一讲java注解的原理吗？**

> 注解本身是一个继承了 `Annotation` 的特殊接口，其具体实现类是Java运行时生成的动态代理类。
>
> 我们通过反射获取注解时，返回的是Java运行时生成的动态代理对象。通过代理对象调用自定义注解的方法，会最终调用`AnnotationInvocationHandler`的`invoke`方法。该方法会从`memberValues`这个 Map 中索引出对应的值。而`memberValues`的来源是 Java 常量池。
>
> 
> 获取接口的时候会创建代理对象



