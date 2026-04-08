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









# 三、集合

==注意== ： 在Java中应该使用小写的`null`来表示空引用。大写的`NULL`不是Java的关键字或内置常量，不应该在代码中使用。



## 单链集合



在学习之前，在这里补充一下会使用到的数据结构：

- 数组：数组的寻址公式：`baseAddress`（首地址） + i * `dataTypeSize`(数据类型大小)；

  

  **为什么数组寻址的索引不从1开始，而是从0开始呢？**

  > 如果寻址的索引从下标一开始，寻址公式就会变化，`baseAddress` + (i - 1) * `dataTypeSize`; 这里应该看出什么区别了吧，就是：i - 1.
  >
  > 这里会让`cpu`额外多出一次减法运算。性能就没那么好了。



### List系列集合

List是一个有序的集合，可以包含重复的元素

- 元素可以重复

- 元素有固定的顺序，即元素的插入顺序

- 可以通过索引访问元素



#### `ArrayList`

``` java
//这里是ArrayList的部分源码。（成员变量和构造方法）
public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable
{
    private static final long serialVersionUID = 8683452581122892189L;

    /** 
     * 默认的数组大小容量，也就是下面的elementData数组的初始容量。
     */
    private static final int DEFAULT_CAPACITY = 10;

    /**
     * 用于空实例的共享空数组实例
     */
    private static final Object[] EMPTY_ELEMENTDATA = {};

    /**
     * 共享空数组实例用于默认大小的空实例。
     * 我们将其与EMPTY_ELEMENTDATA区分开来，以了解添加第一个元素时要膨胀多少。
     */
    private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};

    /**
     * 存储ArrayList元素的数组缓冲区。
     * ArrayList的容量是此数组缓冲区的长度。任何
     * 空数组列表，元素数据==DEFAULTCAPACITY_ELEMENTDATA
     * 当添加第一个元素时，将扩展为DEFAULT_CAPACITY。
     * 真正的存储位置。
     */
    transient Object[] elementData; // non-private to simplify nested class access

    /**
     * The size of the ArrayList (the number of elements it contains).
     * ArrayList集合的大小（大小指的是包含元素个数，不是集合底层的数组大小）
     * @serial
     */
    private int size;

    /**
     * Constructs an empty list with the specified initial capacity.
     *
     * @param  initialCapacity  the initial capacity of the list
     * @throws IllegalArgumentException if the specified initial capacity
     *         is negative
     * 带初始化容量的构造方法。
     */
    public ArrayList(int initialCapacity) {
        if (initialCapacity > 0) {
            //创建指定大小的数组。
            this.elementData = new Object[initialCapacity];
        } else if (initialCapacity == 0) {
            //赋值为默认的空数组。
            this.elementData = EMPTY_ELEMENTDATA;
        } else {
            throw new IllegalArgumentException("Illegal Capacity: "+
                                               initialCapacity);
        }
    }

    /**
     * Constructs an empty list with an initial capacity of ten.
     * 无参的构造方法，创建默认空集合。
     */
    public ArrayList() {
        this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
    }

    /**
     * Constructs a list containing the elements of the specified
     * collection, in the order they are returned by the collection's
     * iterator.
     *
     * @param c the collection whose elements are to be placed into this list
     * @throws NullPointerException if the specified collection is null
     */
    public ArrayList(Collection<? extends E> c) {
        //集合转成数组
        Object[] a = c.toArray();
        //判断数组长度
        if ((size = a.length) != 0) {
            if (c.getClass() == ArrayList.class) {
                elementData = a;
            } else {
                //这个api的作用就是拷贝a数组中的size个元素，然后把数组地址赋值给elementData，数组类型为Object[]类型
                elementData = Arrays.copyOf(a, size, Object[].class);
            }
        } else {
            // replace with empty array.
            elementData = EMPTY_ELEMENTDATA;
        }
    }
}
```



##### 第一次添加和扩容操作

``` java
//add的源码，E就是集合中存储数据的类型 -- ArrayList<E>
	
	/** 方法中调用的方法
     * This helper method split out from add(E) to keep method
     * bytecode size under 35 (the -XX:MaxInlineSize default value),
     * which helps when add(E) is called in a C1-compiled loop.
     * @param e 加入集合的元素
     * @param elementData 集合底层的数组
     * @param s 当前插入数组的位置（索引）
     */
    private void add(E e, Object[] elementData, int s) {
        //比较
        if (s == elementData.length)
            elementData = grow();
        elementData[s] = e;
        size = s + 1;//size表示已经存储的元素个数
    }

    /** 常用的方法
     * Appends the specified element to the end of this list.
     *
     * @param e element to be appended to this list
     * @return {@code true} (as specified by {@link Collection#add})
     */
    public boolean add(E e) {
	    //modCount是什么呢？
        modCount++;
        add(e, elementData, size);
        //总是返回true的。
        return true;
    }

    /**
     * Inserts the specified element at the specified position in this
     * list. Shifts the element currently at that position (if any) and
     * any subsequent elements to the right (adds one to their indices).
     *
     * @param index index at which the specified element is to be inserted
     * @param element element to be inserted
     * @throws IndexOutOfBoundsException {@inheritDoc}
     */
    public void add(int index, E element) {
        rangeCheckForAdd(index);
        modCount++;
        final int s;
        Object[] elementData;
        if ((s = size) == (elementData = this.elementData).length)
            elementData = grow();
        System.arraycopy(elementData, index,
                         elementData, index + 1,
                         s - index);
        elementData[index] = element;
        size = s + 1;
    }
```



第一次添加元素：

![](C:\Users\heban\Desktop\java简历and面试指北\bagu\assets\ArrayList集合第一次扩容流程.png)

集合满了之后再添加元素：

![](C:\Users\heban\Desktop\java简历and面试指北\bagu\assets\ArrayList集合达到数组最大容量的扩容流程.png)



##### **`ArrayList`底层的实现原理是什么？**

- `ArrayList`底层是使用动态的数组实现的。
- `ArrayList`的默认初始化大小是0，当第一次添加元素之后数组的大小会扩容为10。
- `ArrayList`在扩容的时候会进行判断，判断标准由两个参数决定。一个是目前至少需要扩容多大，另一个是当前数组容量的一半。选出这两个数中的较大值，然后由原数组大小加上选出的扩容大小，就是扩容后的数组大小。
- `ArrayList`在添加元素时：
  - 确保数组目前存储元素数量是否等于数组长度，如果等于就进行扩容处理。小于就直接添加进数组。



##### **`ArrayList list = new ArrayList<>(10);`扩容了几次？**

其实没有进行扩容，看了`ArrayList`的构造方法之后就懂了，在指定了集合大小后（除了零），底层是会直接创建一个对应大小的数组，而不是使用成员变量`DEFAULTCAPACITY_EMPTY_ELEMENTDATA`或是`EMPTY_ELEMENTDATA`。



##### **数组和List之间的转化**

1. 数组转`List`
   使用JDK中`Arrays`工具类就行了

   ``` java
   Integer[] arr = {1,2,3};
   List<Integer> list1 = Arrays.asList(arr);//注意数组的类型需要是引入类型
   System.out.println(list1.get(0));
   ```

2. `List`转数组

   ``` java
   //注意toArray中的数组一定要指定类型和大小。
   Integer[] array = list1.toArray(new Integer[3]);
   for (Integer i : array) {
       System.out.println(i);
   }
   ```

**灵魂拷问：**

**如果修改了原数组`arr`，那么`list`会受到影响吗？**

> 会的。list会受到影响，先思考下为什么？这里需要想到 List 的构造方法。`ArrayList`的构造方法。哈哈哈，其实这样的，还是需要看`Arrays`工具类是怎么实现的
> ``` java
> private static class ArrayList<E> extends AbstractList<E>
>         implements RandomAccess, java.io.Serializable
>     {
>         private static final long serialVersionUID = -2764017481108945198L;
>         private final E[] a;
> 
>         ArrayList(E[] array) {
>             a = Objects.requireNonNull(array);
>         }
>     
>     //此处忽略源码的其他代码
> }
> ```
>
> `Arrays`工具类底层是在这个工具类中有一个`ArrayList`子类，这个子类和原来的`ArrayList`并不太一样，他只是一个数组。只是简单的赋值操作，`Arrays`中的`ArrayList`底层的数组和传入的数组指向的是同一个内存空间。原数组修改，`list`中的数据也会对应的修改。

**如果修改了List中的内容，数组会有影响吗？**

> 这里就不要上当了，直接看源码，这里的源码是`ArrayList`类中的源码，并不是`Arrays`工具类中的`ArrayList`中的源码：
>
> ``` java
> public Object[] toArray() {
>     return Arrays.copyOf(elementData, size);
> }
> ```
>
> 所以还是需要看`Arrays`工具类
> ``` java
>     //先是执行这个方法
>     public static <T> T[] copyOf(T[] original, int newLength) {
>         return (T[]) copyOf(original, newLength, original.getClass());
>     }
>     //再执行这个方法
>     @HotSpotIntrinsicCandidate
>     public static <T,U> T[] copyOf(U[] original, int newLength, Class<? extends T[]> newType) {
>         @SuppressWarnings("unchecked")
>         T[] copy = ((Object)newType == (Object)Object[].class)
>             ? (T[]) new Object[newLength]
>             : (T[]) Array.newInstance(newType.getComponentType(), newLength);
>         System.arraycopy(original, 0, copy, 0,
>                          Math.min(original.length, newLength));
>         return copy;
>     }
> ```
>
> 数组不会受到影响，因为在底层是重新创建了一个新数组。



##### remove方法

源码：

``` java
	//下面这两个方法都是ArrayList类中的源码
	public E remove(int index) {
        Objects.checkIndex(index, size);
        final Object[] es = elementData;

        @SuppressWarnings("unchecked") E oldValue = (E) es[index];
        fastRemove(es, index);

        return oldValue;
    }

    private void fastRemove(Object[] es, int i) {
        modCount++;
        final int newSize;
        if ((newSize = size - 1) > i)//这里是判断需要删除的元素是不是最后一个
            System.arraycopy(es, i + 1, es, i, newSize - i);//
        es[size = newSize] = null;//把之前最后一个元素置为null
    }
	
	
	/**
	 * @param      src      the source array. 原数组
     * @param      srcPos   starting position in the source array. 原数组中的开始复制的位置
     * @param      dest     the destination array. 需要复制到的数组
     * @param      destPos  starting position in the destination data. 需要复制元素的开始起点
     * @param      length   the number of array elements to be copied. 复制完的数组的长度
	*/
	//这个方法是System.java类中的了
	@IntrinsicCandidate
    public static native void arraycopy(Object src,  int  srcPos,
                                        Object dest, int destPos,
                                        int length);

例子：
int[] src = {10, 20, 30, 40};
int[] dest = {0, 0, 0, 0};

System.arraycopy(src, 1, dest, 2, 2);
        
dest = {0, 0, 20, 30}
        
```

**删除元素并不会改变集合底层数组对象，只是把底层的数组元素挪动了位置**






#### `LinkedList`

底层是一个双向链表

``` java
public class LinkedList<E>
    extends AbstractSequentialList<E>
    implements List<E>, Deque<E>, Cloneable, java.io.Serializable
{
    transient int size = 0;

    /**
     * Pointer to first node.
     */
    transient Node<E> first;

    /**
     * Pointer to last node.
     */
    transient Node<E> last;
    
	//双向链表中的Node源码    
    private static class Node<E> {
        E item;
        Node<E> next;
        Node<E> prev;

        Node(Node<E> prev, E element, Node<E> next) {
            this.item = element;
            this.next = next;
            this.prev = prev;
        }
    }
    
}
```



#### `LinkedList`和`ArrayList`的区别

- 底层数据结构
  - `ArrayList`是动态数组的数据结构实现
  - `LinkedList`是双向链表的数据结构实现
- 操作数据效率
  - `ArrayList`按照下标查询的时间复杂度是O(1)【内存是连续的空间，根据寻址公式获取元素】，`LinkedList`不支持下标查询。
  - 查询（未知索引）：两个集合都需要遍历，时间复杂度都是O(1)。
  - 新增和查询：
    - `ArrayList`尾部的插入和删除时间复杂度是O（1），其他的部分增删需要挪动数组，时间复杂度是O（n）。
    - `LinkedList`头尾节点的增删时间复杂度是O（1），其他的部分都需要先遍历一遍查询到对应的节点后再进行删除，时间复杂度为O（n）。 
- 内存空间占用
  - `ArrayList`底层是数组，空间连续，节省内存
  - ：`inkedList`是双向链表来存储数据，和两个指针，更占用内存。

- 线程安全
  - 两个集合都不是线程安全的
  - 如果想实现线程安全，可以作为局部变量在方法内使用进行使用。也可以进行包装，`Collections.synchronizedList(new ArrayList<>())`后进行使用。






### Set系列集合

 Set是一个不允许有重复元素的集合

- 元素唯一、没有重复的元素
- 元素没有固定的顺序，即元素的实际顺序和插入顺序不一定是一样的
- 不能通过索引访问集合中的元素





```java
Set<String> s = new HashSet<>();

boolean r1 = s.add("张三");
boolean r2 = s.add("张三");
boolean r3 = s.add("李四");
boolean r4 = s.add("王五");

//无序的
//System.out.println(s);//[李四, 张三, 王五]
//不重复
//只有一个张三

//使用迭代器遍历集合
Iterator<String> it = s.iterator();
while (it.hasNext()) {
    String str = it.next();
    System.out.println(str);
}

//使用增强for
for (String string : s) {
    System.out.println(string);
}

//使用lambda表达式
s.forEach(string -> System.out.println(string));

```



#### `HashSet`

无序、不重复、无索引

##### HashSet底层原理

​	底层采用哈希表存储数据

​	哈希表是一种对于增删查改数据性能都较好的结构

###### 哈希表的组成

​	JDK8之前：数组 + 链表

​	JDK8开始：数组 + 链表 + 红黑树

​	

###### 哈希值

- 根据`hashCode`方法算出来的int类型的整数，对象调用`hashCode()`方法会返回一个整数，这个整数就是哈希值
- 该方法定义在Object类中，所有的对象都可以调用，默认使用地址值进行计算
- 一般情况下，会重写`hashCode`方法，利用对象内部的属性值计算哈希值

 默认是用地址值算，重写了之后就是用属性值算



###### 对象的哈希值特点

- 如果没有重写`hashCode`方法，不同对象计算出的哈希值是不同的（因为没有重写是使用地址值计算的，重写之后使用属性值进行计算）
- 如果已经重写了`hashCode`方法，不同的对象只要属性值相同，计算出的哈希值就是一样的
- 在小部分情况下，不同的属性值或者不同的地址值计算出的哈希值也有可能是一样的（哈希碰撞）



```java
//1.创建对象
student s1 = new student("zhangsan",23);
student s2 = new student("zhangsan",23);
student s3 = new student("zhangsan",23);

//2.如果没有重写hashCode方法，不同对象计算出的哈希值是不一样的
System.out.println(s1.hashCode());//793589513
System.out.println(s2.hashCode());//1313922862

//按ALT + Insert键可以快速生成重写方法
//此时为重写后的代码实现
System.out.println(s1.hashCode());//-1461067292
System.out.println(s2.hashCode());//-1461067292

//小部分，不同的属性值或者不同的地址值计算出的哈希值也有可能是一样的
//哈希碰撞
System.out.println("abc".hashCode());//96354
System.out.println("acD".hashCode());//96354
```



###### `HashSet`JDK8以前的底层原理

1. ​	创建一个默认长度16，默认加载因子为0.75的数组，数组名为table

   此时数组中什么都没有存，全部是null

   这里的默认加载因子是数组的扩容时机，当数组元素达到总容量的0.75后会扩容到原先容量的两倍

   当链表的长度大于8而且数组的长度大于等于64时，当前的链表就会自动的转为红黑树

   ```java
   HashSet<String> hm = new HashSet<>();
   ```

2. 根据元素的哈希值跟数组的长度计算出应存入的位置

   ```java
   int index = (数组长度 - 1) & 哈希值;
   ```

3. 判断当前位置是否为null，如果是null直接存入

4. 如果位置不为null，表示有元素，则调用equals方法比较属性值

5. 一样：不存        不一样：存入数组，形成链表

   JDK8以前：新元素存入数组，老元素挂在新元素的下面

   JDK8开始：新元素直接挂在老元素的下面

==注意==：如果集合中存储的时自定义对象，必须重写`hashCode`和`equals`方法，这两个方法默认使用地址值进行计算、比较的



###### HashSet为什么存和取的顺序不一样？

table数组可能存的是一个链表或者一颗红黑树还或者只是单个元素

又因为元素添加时如果添加位置有元素，需要添加的元素（数组中没有这个元素）就会挂在添加位置的下面形成链表，数组和链表长度足够后就会转成红黑树

可是正因为是挂上去的，可以是0索引处是第一个添加的元素，然后在8索引处添加第二个元素，再添加时如果又是添加到0索引处就会直接挂在0索引元素的下面形成链表（也有可能是添加到红黑树的情况类似）

在读取数组时是按数组索引来的，读取0索引的元素、链表、红黑树，现在假设是按上面形成的链表，则是读取第一个元素，在读取第三个添加的元素，在读取到第二次添加的元素

所以说存和取的顺序是不同的



###### HashSet为什么没有索引？

因为HashSet里面有链表又有红黑树，应该定义谁为零索引呢？是不好定义的，所以没有索引



###### HashSet是利用什么机制保证去重的？

利用`HashCode`方法和`equals`方法，利用`HashCode`方法就可以得到哈希值，而得到哈希值就可以知道该存在哪个位置，再调用`equals`方法比较内部属性值，如果属性值相同就不会存入

```java
//利用HashSet集合去除重复元素
//创建一个学生对象的集合，存储多个学生对象
//使用程序实现在控制台遍历集合
//要求：学生对象的成员变量属性值相同，我们就认为是同一个对象

//创建学生对象
student s1 = new student("zhangsan",23);
student s2 = new student("lisi",22);
student s3 = new student("wangwu",21);
student s4 = new student("zhangsan",23);
//创建集合用来添加学生对象
HashSet<student> set = new HashSet<>();
/*
//没有重写student类中HashCode方法和equals方法前提下添加学生对象
System.out.println(set.add(s1));//true
System.out.println(set.add(s2));//true
System.out.println(set.add(s3));//true
System.out.println(set.add(s4));//true
//打印集合
System.out.println(set);
//[student{name = wangwu, age = 21}, student{name = zhangsan, age = 23}, student{name = lisi, age = 23}, student{name =zhangsan, age = 23}]
*/

//重写student类中HashCode方法和equals方法前提下添加学生对象
System.out.println(set.add(s1));//true
System.out.println(set.add(s2));//true
System.out.println(set.add(s3));//true
System.out.println(set.add(s4));//false
//打印集合
System.out.println(set);
//[student{name = lisi, age = 23}, student{name = zhangsan, age = 23}, student{name = wangwu, age = 21}]

```



#### `LinkedHashSet`

有序、不重复、无索引

这里的有序是指保证存储和取出的元素顺序一致

==注意== ： 如果要求去重并且存取有序，才会使用`LinkedHashSet`，`LinkHashSet`在哈希表的基础上有多做了一些事情，导致运行效率变低，除了这种情况一般还是使用`HashSet`

`LinkedHashSet`继承`HashSet`，方法可以按`HashSet`的使用



###### `LinkedHashSet`底层原理

原理：底层数据结构依然是哈希表，只是每个元素有额外的多了一个双链表的机制记录存储的顺序

遍历时是按双向链表来遍历的，这样才会是的输出和存储时的顺序一样

```java
//创建集合存放学生对象
LinkedHashSet<student> lhs = new LinkedHashSet<>();
//创建学生对象
student s1 = new student("zhangsan",23);
student s2 = new student("lisi",22);
student s3 = new student("wangwu",21);
student s4 = new student("zhangsan",23);
//添加学生对象
System.out.println(lhs.add(s3));//true
System.out.println(lhs.add(s2));//true
System.out.println(lhs.add(s1));//true
System.out.println(lhs.add(s4));//false
//打印集合
System.out.println(lhs);
//有顺序的
//[student{name = wangwu, age = 21}, student{name = lisi, age = 22}, student{name = zhangsan, age = 23}]
```



#### `TreeSet`

可排序、不重复、无索引

可排序：按照元素的默认规则（有小有大）排序。

`TreeSet`集合底层是基于红黑树的数据结构实现的排序，增删改查性能较好

打印`TreeSet`对象的话就会按照排序规则来打印



```java
//利用TreeSet存储整数并进行排序
//创建TreeSet集合对象
TreeSet<Integer> ts = new TreeSet<>();
//添加元素
ts.add(5);
ts.add(2);
ts.add(3);
ts.add(1);
ts.add(4);
//打印集合
System.out.println(ts);//[1, 2, 3, 4, 5]----有序的
```





##### `TreeSet`集合默认的规则

- 对于数值类型：Integer、Double，默认按照从小到大的顺序进行排序
- 对于字符、字符串类型：按照字符在ASCII码表中的数字升序进行排序

##### `TreeSet`的两种比较方式

- 方式一：

  `javabean`类实现`Comparable`接口指定比较规则

  默认的排序规则/自然排序

  student（自己写的那个类）实现`Comparable`接口，重写里面的抽象方法，再指定比较规则

  ```java
  @Override
  public int compareTo(student o) {
      return this.getAge() - o.getAge();
      //这串代码中
      //this表示当前要添加的元素
      //o表示已经在红黑树存在的元素
      //返回值
      //负数：认为要添加的元素是小的，存左边
      //正数：认为要添加的元素是大的，存右边
      //零：认为要添加的元素已经存在，舍弃不存
      
  }
  ```



- 方式二：

  比较器排序：创建`TreeSet`对象的时候，传递比较器`Comparator`指定规则

  ```java
  //要求：按照字符串长度进行比较，如果长度相同，再按首字母排序
  //这个要求字符串的CompareTo方法就不能满足了，所以需要使用比较器排序
  /*
  TreeSet<String> ts = new TreeSet<>(new Comparator<String>() {
      //o1表示当前需要添加的元素
      //o2表示已经在红黑树中存在的元素
      @Override
      public int compare(String o1, String o2) {
          //按照长度排序
          int i = o1.length() - o2.length();
          //如果长度相同就按照首字母进行排序
          i = i == 0 ? o1.compareTo(o2) : i;
          return i;
      }
  });
  */
  //Comparator接口是函数式接口可以使用lambda表达式来简写
  TreeSet<String> ts = new TreeSet<>((o1, o2) -> {
          //按照长度排序
          int i = o1.length() - o2.length();
          //如果长度相同就按照首字母进行排序
          i = i == 0 ? o1.compareTo(o2) : i;
          return i;
      }
  );
  
  ts.add("c");
  ts.add("ab");
  ts.add("df");
  ts.add("qwer");
  
  System.out.println(ts);
  //没有使用比较器得到的结果 [ab, c, df, qwer]
  //使用比较器得到的结果[c, ab, df, qwer]
  ```



==使用原则== ： 默认使用第一种，如果第一种不能满足当前需求，就是用第二种 

==注意== : 如果方式一和方式二同时存在，会优先使用方式二来排序，





##### `TreeSet`综合小练习

```java
  /*
          要求：
          创建学生对象五个
          属性：姓名、年龄、语文成绩、英语成绩、数学成绩
          按照总分从高到低输出到控制台
          如果总分一样，按照语文成绩排序
          如果语文成绩一样，按照数学成绩排序
          如果数学成绩一样，按照英语成绩排序
          如果英语成绩一样，按照年龄排序
          如果年龄一样，按照姓名的字母顺序排序
          如果都一样，认为是同一个学生，不存
   */

	//创建集合
	//一般默认都是用ArrayList，比较常见
	//如果想要数据唯一，就可以从Set系列集合中选择
	//想要数据唯一，可以考虑HashSet
	//如果即想要数据唯一又想要排序就可以使用TreeSet

  //要求排序，那我就选择TreeSet,现在按照比较器的方法进行排序
/*  
TreeSet<student> ts = new TreeSet<>(new Comparator<student>() {
      @Override
      public int compare(student o1, student o2) {
          //o1是当前需要添加的元素
          //o2是在红黑树中已经存在的元素
          int i = (o1.getChinese() + o1.getEnglish() + o1.getMath()) - ((o2.getChinese()) + o2.getEnglish() + o2.getMath());
          if (i == 0) {
              //现在按照语文成绩比
              i = o1.getChinese() - o2.getChinese();
              if (i == 0) {
                  //按照数学成绩排序
                  i = o1.getMath() - o2.getMath();
                  if (i == 0) {
                      //按照英语成绩排序
                      i = o1.getEnglish() - o2.getEnglish();
                      if (i == 0) {
                          //按照年龄排序
                          i = o1.getAge() - o2.getAge();
                          if (i == 0) {
                              //按照姓名的字母顺序排序
                              i = o1.getName().length() - o2.getName().length();
                          }
                      }
                  }
              }
          }
          return -i;
      }
  });
  */
 TreeSet<student> ts = new TreeSet<>(new Comparator<student>() {
        @Override
        public int compare(student o1, student o2) {
            //o1是当前需要添加的元素
            //o2是在红黑树中已经存在的元素
            int i = (o1.getChinese() + o1.getEnglish() + o1.getMath()) - ((o2.getChinese()) + o2.getEnglish() + o2.getMath());
            i = i == 0 ? o1.getChinese() - o2.getChinese() : i;
            i = i == 0 ? o1.getMath() - o2.getMath() : i;
            i = i == 0 ? o1.getEnglish() - o2.getEnglish() : i;
            i = i == 0 ? o1.getAge() - o2.getAge() : i;
            i = i == 0 ? o1.getName().length() - o2.getName().length() : i;

            return -i;
        }
  });
  //创建五个学生对象
  student s1 = new student("zhangsan",23,90,99,50);//239
  student s2 = new student("lisi",24,90,98,50);//238
  student s3 = new student("wangwu",25,95,100,30);//225
  student s4 = new student("zhaoliu",26,60,99,70);//229
  student s5 = new student("qianqi",26,70,80,70);//220
  //添加对象
  ts.add(s1);
  ts.add(s2);
  ts.add(s3);
  ts.add(s4);
  ts.add(s5);
  //打印集合
//System.out.println(ts);
  for (student t : ts) {
      System.out.println(t);
  }
/*
student{name = zhangsan, age = 23, chinese = 90, math = 99, english = 50}
student{name = lisi, age = 24, chinese = 90, math = 98, english = 50}
student{name = zhaoliu, age = 26, chinese = 60, math = 99, english = 70}
student{name = wangwu, age = 25, chinese = 95, math = 100, english = 30}
student{name = qianqi, age = 26, chinese = 70, math = 80, english = 70}
*/


```



### 使用场景 ：

1. 如果想要集合中元素可重复
   - 使用`ArrayList`集合，基于数组的。（用的最多）
2. 如果想要集合中的元素可重复，并且增删操作明显多于查询
   - 用`LinkedList`集合，基于链表的。
3. 如果想对集合中的元素去重
   - 用HashSet集合，基于哈希表的。（用的最多）
4. 如果想要对集合中的元素去重，并且保证存取顺序
   - 用`LinkedHashSet`集合，基于哈希表和双链表，效率低于`HashSet`
5. 如果想要对集合中元素进行排序
   - 用`TreeSet`集合，基于红黑树，后序也可以使用`List`集合实现排序



### `Queue`集合



#### `PriorityQueue`集合

`PriorityQueue`类提供堆数据结构的功能。**默认是最小堆**

与普通队列不同，优先队列元素是按排序顺序检索的。

假设我们想以升序检索元素。在这种情况下，优先队列的头是最小的元素。检索到该元素后，下一个最小的元素将成为队列的头。

**需要注意的是，优先队列的元素可能没有排序。但是，元素总是按排序顺序检索的。**



##### 构造方法

```java
PriorityQueue<Integer> p = new PriorityQueue<>();
//在括号里面可以指定比较器
PriorityQueue<Integer> p1 = new PriorirtQueue<>((a,b) -> a - b);//这是默认的，最小堆
//这个比较器的规则是（个人认为）：返回值小于零时，选出第一个数a，类似与这种。
```



##### 添加元素方法

- add() - 将指定的元素插入队列。如果队列已满，则会引发异常。
- offer() - 将指定的元素插入队列。如果队列已满，则返回false。





##### 访问元素

要从优先级队列访问元素，我们可以使用peek()方法。此方法返回队列的头部。



##### 删除元素

- remove() - 从队列中删除指定的元素
- poll() - 返回并删除队列的开头



##### 遍历

`PriorityQueue` 是一个基于堆的数据结构，它并不保证元素的迭代顺序与优先级顺序一致。因此，遍历 `PriorityQueue` 时需要注意以下几点：

1. **迭代器遍历**：

   - 使用 `for-each` 循环或 `Iterator` 遍历 `PriorityQueue` 时，元素的顺序是不确定的。这是因为 `PriorityQueue` 的内部实现是一个堆，而堆的遍历顺序并不是按照优先级顺序排列的。

   - 示例代码：

     ```java
     PriorityQueue<Integer> pq = new PriorityQueue<>();
     pq.add(3);
     pq.add(1);
     pq.add(4);
     pq.add(1);
     pq.add(5);
     
     for (int num : pq) {
         System.out.println(num);
     }
     ```

     输出结果可能是：`1, 1, 3, 4, 5` 或其他顺序，但不一定是按照优先级顺序。

     

     ```java
     import java.util.PriorityQueue;
     import java.util.Iterator;
     
     class Main {
         public static void main(String[] args) {
     
             //创建优先级队列
             PriorityQueue<Integer> numbers = new PriorityQueue<>();
             numbers.add(4);
             numbers.add(2);
             numbers.add(1);
             System.out.print("使用iterator()遍历PriorityQueue : ");
     
             //使用iterator()方法
             Iterator<Integer> iterate = numbers.iterator();
             while(iterate.hasNext()) {
                 System.out.print(iterate.next());
                 System.out.print(", ");
             }
         }
     }
     ```

     输出结果：

     ```tex
     使用iterator()遍历PriorityQueue : 1, 4, 2,
     ```

     

2. **按优先级顺序遍历**：

   - 如果需要按照优先级顺序遍历 `PriorityQueue`，可以使用 `poll()` 或 `remove()` 方法依次取出队列中的元素。

   - 示例代码：

     ```java
     PriorityQueue<Integer> pq = new PriorityQueue<>();
     pq.add(3);
     pq.add(1);
     pq.add(4);
     pq.add(1);
     pq.add(5);
     
     while (!pq.isEmpty()) {
         System.out.println(pq.poll());
     }
     ```

     

     输出结果是：`1, 1, 3, 4, 5`，按照优先级顺序输出。

### 总结

- **添加数据**：`PriorityQueue` 通过 `add` 或 `offer` 方法添加元素，并根据自然顺序或比较器调整堆结构。
- **遍历**：使用迭代器遍历时，顺序不确定；若需要按优先级顺序遍历，应使用 `poll()` 或 `remove()` 方法依次取出元素。遍历顺序和优先级顺序是不一定相同的，优先级顺序是集合根据比较器规则进行排序后的顺序，



##### PriorityQueue其他方法 

| 方法              | 内容描述                                                     |
| :---------------- | :----------------------------------------------------------- |
| contains(element) | 在优先级队列中搜索指定的元素。如果找到该元素，则返回true，否则返回false。 |
| size()            | 返回优先级队列的长度。                                       |
| toArray()         | 将优先级队列转换为数组，并返回它。                           |











## 双列集合



### 双列集合特点：

- 双列集合一次需要存一对数据，分别为键和值
- 键是不能重复的，值是可以重复的
- 键和值是一一对应的，每一个键只能找到自己对应的值
- 键 + 值这个整体我们称之为 “键值对” 或者 “键值对对象” ，在Java中叫做“Entry对象” 
- 元素没有固定的顺序，即插入顺序和集合中实际顺序可能是不一样的



### `Map`接口



#### `Map`的常见API

Map是双列集合的顶层==接口==，它的功能是全部双列集合都可以继承使用的

```java
public interface Map<K, V> 
```

Map接口是有两个泛型的



| 方法名称                              | 说明                                 |
| ------------------------------------- | ------------------------------------ |
| `V put (K key,V value)`               | 添加元素/覆盖                        |
| `V remove(Object key)`                | 根据键删除键值对元素                 |
| `void clear()`                        | 移除所有的键值对元素                 |
| `boolean containsKey (Object key)`    | 判断集合是否包含指定的键             |
| `boolean containsValue(Object value)` | 判断集合是否包含指定的值             |
| `boolean isEmpty()`                   | 判断集合是否为空                     |
| `int size()`                          | 集合的长度，也就是集合中键值对的个数 |

==注意== ： 在Map中的方法名与Collection中的方法名有一些不同，如添加的方法名，Collection中是add，在Map中就是put。



```java
Map<String,String> m = new HashMap<>();
//put方法细节
//添加/覆盖
//在添加元素时，如果键不存在，那么直接把键值对对象添加到Map集合当中，返回null
//在添加元素时，如果键时存在的，那么会把原来的键值对对象覆盖，会把被覆盖的值进行返回。

m.put("郭靖","黄蓉");
String str1 = m.put("韦小宝","沐剑屏");
System.out.println(str1);//null

m.put("尹志平","小龙女");
String str2 = m.put("韦小宝","双儿");
System.out.println(str2);//沐剑屏

System.out.println(m);//{韦小宝=双儿, 尹志平=小龙女, 郭靖=黄蓉}

//删除
String str3 = m.remove("郭靖");
System.out.println(str3);//黄蓉

System.out.println(m);//{韦小宝=双儿, 尹志平=小龙女}


//清空
m.clear();
System.out.println(m);//{}

```



#### `HashMap`集合

1. `HashMap`是`Map`里面的一个实现类
2. 没有额外需要学习的特有方法，直接使用`Map`里面的方法就可以了
3. 特点都是由键决定的：无序、不重复、无索引
4. `HashMap`跟`HashSet`底层原理是一样的，都是哈希表结构





##### 底层原理

- 在put添加元素时，会创建一个`Entry`对象，并利用`Entry`对象里面的==键==来计算哈希值，跟值无关，计算出在数组中应存入位置的索引
- 如果计算出索引位置为null就直接添加进去了，如果不是null，而是已经有元素了，就会与其比较==键==是否相同，如果键相同就会进行覆盖，键不相同就会挂在该位置下面（挂的方式看JDK版本）。其余与HashSet底层原理差不多（或者说一样）。



##### 源码分析

在`HashMap`集合中每一个元素都是一个`Node`类（`Node`为`HashMap`的内部类）

###### `Node`类源码（链表中的键值对象）

```java
//Node类实现了Entry接口，也就是说，一个Node类就是一个键值对
static class Node<K,V> implements Map.Entry<K,V> {
        final int hash;//通过键算出来的哈希值
        final K key;//键
        V value;//值
        Node<K,V> next;//什么时候用到next？
    	//当底层数组某个索引存有元素且还需要在该索引处添加元素，此时就需要用到next了，新添加的元素会挂在原来元素的下面，
    	//原来元素的next就会储存新元素（结点）的地址来找到下一个元素

    	.....//代码省略
    }
```



###### `table`

`table`就是底层存储数据的数组或者说这个`table`存储了底层数组的地址值

创建`HashMap`集合时，`table`数组值是null，当添加元素时会创建一个数组

```java
transient Node<K,V>[] table;//源码，这里没有赋值，所以默认值为null
```

**（补充）：`transient`关键字的主要作用就是让某些被transient关键字修饰的成员属性变量不被序列化**

###### 红黑树中的键值对对象

```java
static final class TreeNode<K,V> extends LinkedHashMap.Entry<K,V> {
        TreeNode<K,V> parent;  // red-black tree links，父节点的地址值
        TreeNode<K,V> left;//左子节点的地址值
        TreeNode<K,V> right;//右子节点的地址值
        TreeNode<K,V> prev;    // needed to unlink next upon deletion
        boolean red;//节点的颜色
        TreeNode(int hash, K key, V val, Node<K,V> next) {
            super(hash, key, val, next);
        }
		
    	......//代码省略
        }
```



###### `put`

添加元素的时候至少考虑三种情况

1. 数组位置为null
2. 数组位置不为null，键不重复，挂在下面形成链表或者红黑树
3. 数组位置不为null，键重复，元素覆盖

```java
//参数一：键
//参数二：值
//返回值：被覆盖元素的值，如果没有覆盖，返回null
public V put(K key, V value) {
        return putVal(hash(key), key, value, false, true);
}
```



```java
//利用键计算出对应的哈希值，再把哈希值进行一些额外的处理
//简单理解：返回值就是返回键的哈希值
static final int hash(Object key) {
    int h;
    return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
}
```



```java
final V putVal(int hash, K key, V value, boolean onlyIfAbsent,boolean evict) {
	//定义一个局部变量，因为开始定义的成员变量是储存在堆空间中，而在putVal如果需要使用的话就需要频繁进入堆空间调用
    //会使得效率变低
    Node<K,V>[] tab;
    //临时的第三方变量，用来记录键值对对象的地址值
    Node<K,V> p;
    //表示当前数组的长度
    int n；
    //表示索引（index）
    int i;
    //把哈希表中数组的地址值赋值给局部变量tab，
    tab = table;
    
    //第一次赋值时table还是null，所以tab也会被赋值为null
    if (tab == null || (n = tab.length) == 0){
        //下面是什么情况下会使用resize()方法
        //1.如果当前是第一次添加数据，底层会创建一个默认长度为16，加载因子为0.75的数组
        //2.如果不是第一次添加数据，就会看数组中的元素是否达到了扩容的条件
        //如果没有达到扩容的条件，底层不会做任何操作
        //如果达到了扩容条件，底层会把数座扩容成原来的两倍，并把数据全部(包括链表和红黑树)转移到新的哈希表中
        tab = resize();
        //resize应该是有很多作用，在这里只需要使用1.这个作用，最后代码那里可能是使用判断是否需要扩容的作用
        
    	//把当前数组的长度赋值给n
        n = tab.length;
    }
    
    //拿着数组的长度跟键的哈希值进行计算，计算出当前键值对对象会在数组中存入应存入的位置
    i = (n - 1) & hash;//(n - 1) & hash可以代替hash % n的模运算，因为&效率更高，但是代替的前提是n为2的m次幂。
    //获取数组中对应元素的数据
    p = tab[i];
    
    //第一次赋值为null
    if (p == null){
        //底层会创建一个键值对对象，直接放到数组当中
        tab[i] = newNode(hash, key, value, null);//newNode是一个方法
    } else {
        //当前位置已经有了元素
        Node<K,V> e;//这里又新建了一个节点
        K k;
        
        //等等号左边：数组中键值对(刚获取出当前要添加键值对对象应存入位置的原元素，也就是要挂在的那个元素的链表的头节点)的哈希值
        //等等号右边：当前需要添加键值对对象的哈希值
        //键不一样的话就会返回false
        //键一样就会返回true
        boolean b1 = p.hash == hash;
        
        //判断当前需要插入的元素的key是否和头节点的key相同。既然上面已经进行判断是否相同，为什么还需要加上其他条件来判断是否key相同呢？
        //其实是因为防止hash冲突，不同的key也可能是相同的hash值，所以仅仅是hash值相同并不能代表key是相同的。
        //所以在hash值相同的前提下，还需要进行key值的比较。
        //注意，这里是和头节点进行比较
        if ( b1 && ((k = p.key) == key || (key != null && key.equals(k))))
            //进入这个if里面，说明头节点和当前需要插入的元素的key是相同的，进行覆盖。
            e = p;
        else if (p instanceof TreeNode)//判断刚从数组中获取的键值对是不是红黑树中的节点
            //检查元素是否存在，在添加到红黑树的方法中会进行处理
            //如果是红黑树的节点就会添加到红黑树中
            //调用方法putTreeVal，把当前的节点按照红黑树的规则添加到红黑树中
            e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
        else {
            //不是红黑树中的节点
            //表示此时下面挂的是链表
            for (int binCount = 0;/*判断条件没有写默认为true*/ ; ++binCount) {
                //这个if相当于不断往后面找存入位置
                if ((e = p.next) == null) {
                    //此时就会创建一个新的节点，挂在下面形成链表
                    p.next = newNode(hash, key, value, null);
                    //判断当前链表长度是否超过8，如果超过8，就会调用treeifyBin方法
                    //treeifyBin方法底层还会继续判断
                    //如果数组的长度是否大于等于64
                    //如果满足这两个条件，就会把这个链表转成红黑树
                    //static final int TREEIFY_THRESHOLD = 8;
                    if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                        //链表长度大于8
                        treeifyBin(tab, hash);
                    break;
                    //这里的break是因为如果进了这个if就说明p.next为null，找到了在链表中该存入的位置
                    //这是个死循环必须有break跳出循环
                 }
                 if (e.hash == hash && ((k = e.key) == key || (key != null && key.equals(k))))
                  //if里后面调用key.equals方法是为了避免哈希碰撞
                     break;
                 p = e;
            }
        }
        //如果e为null，表示不需要覆盖任何元素
        if (e != null) { // existing mapping for key
            V oldValue = e.value;
            if (!onlyIfAbsent || oldValue == null)//onlyIfAbsent这个是一个boolean类型的，即上面的参数四
                e.value = value;
            afterNodeAccess(e);
            return oldValue;
        }
    }
    
    ++modCount;//并发修改异常相关的
    //threshold:记录的就是数组的长度 * 0.75 , 哈希表的扩容时机 16 * 0.75 = 12
    if (++size > threshold)
        //进行扩容
        resize();
    
    afterNodeInsertion(evict);//与linkedHashMap相关
    
    //当前没有覆盖任何元素，直接返回null
    return null;
}
```

对上面源码的**总结**：

``` tex
初始化一些变量
初始化之后直接判断散列表是否初始化过
1.没有初始化过，直接进行扩容，完成后接着执行 2. 处流程
2.初始化过，接着下面的流程
根据key计算应该存放位置，存放位置 i = (n - 1) & hash;
获取散列表中i处的元素 p = tab[i];
进行判断：
1.p == null
	直接存储新元素
2.p处有元素，接着进行判断
	初始化节点 Node<K,V> e;
	1.判断头节点是否重复，头节点相同, e = p
	2.分支判断是链表还是红黑树
		1.红黑树
			判断是否与树中元素有重复key，有的话 e = 重复节点
		2.链表
			和红黑树差不多的流程，但是区别就是红黑树不会再变化成其他数据结构了，但是链表长度超过8加上散列表长度超过64，就会转化成红黑树
			遍历链表节点，
				1.节点中存在重复节点， e = 重复节点
				2.遍历到链表末尾，没有重复节点，加入链表末尾，进行上面说的判断，是否需要转化成红黑树
				
完成上面的if else
判断e是否为null
e == null 说明没有重复节点，不需要覆盖
e != null 说明有重复节点，需要覆盖

++size > threshold 
yes 扩容
no 不扩容

```







###### 扩容机制

``` java
final Node<K,V>[] resize() {
   	//resize是HashMap中的一个方法，可以直接调用HashMap的成员变量table。
    //把老的散列表保存。
    Node<K,V>[] oldTab = table;
    //定义老的散列表的大小
    int oldCap = (oldTab == null) ? 0 : oldTab.length;
	//定义旧的扩容时机，注意这里是threshold，不是loadFactor。
    int oldThr = threshold;
    //初始化新的散列表大小和扩容时机大小
    int newCap, newThr = 0;
    //判断旧的散列表大小是否大于零，也就是判断散列表是不是未初始化的，new hashmap的时候不指定散列表大小只会初始化加载因子。
    if (oldCap > 0) {
        //static final int MAXIMUM_CAPACITY = 1 << 30;
        //判断数组长度是否超过最长数组长度，这里是一个安全校验
        if (oldCap >= MAXIMUM_CAPACITY) {
            //如果是超过最长数组长度，则直接把扩容阈值设置为int类型的最大值，然后直接返回老数组
            threshold = Integer.MAX_VALUE;
            return oldTab;
        }
        //把新数组的容量扩大两倍，判断扩大后的长度是否超过数组最长长度，没有超过就把扩容阈值也扩大两倍
        else if ((newCap = oldCap << 1) < MAXIMUM_CAPACITY &&
                 oldCap >= DEFAULT_INITIAL_CAPACITY)
            //扩容阈值扩大两倍
            newThr = oldThr << 1; // double threshold
    } else if (oldThr > 0) // initial capacity was placed in threshold
       	//这里的判断是这样的：
        //oldCap <= 0 and oldThr 说明HashMap已经初始化了，可能是把元素全部删除掉了，它的临界值依旧还是存在的
        //如果是首次初始化，这个扩容阈值是0.
        newCap = oldThr;
    else {               // zero initial threshold signifies using defaults
        //进入这里的条件：oldCap <= 0 && oldThr <= 0
        //这里还是有点不懂？执行了构造函数之后，oldThr不应该是DEFAULT_INITIAL_FACTOR吗？DEFAULT_INITIAL_FACTOR的值为0.75f啊
        //这里搞错了，开始以为是把loadFactor赋值给了oldThr，其实上面是把threshold赋值给了oldThr
        //散列表只是执行了构造函数，初始化散列表的容量和扩容时机，默认大小为16
        newCap = DEFAULT_INITIAL_CAPACITY;
        //设置默认值，为12
        newThr = (int)(DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY);
    }
    if (newThr == 0) {
        float ft = (float)newCap * loadFactor;
        newThr = (newCap < MAXIMUM_CAPACITY && ft < (float)MAXIMUM_CAPACITY ?
                  (int)ft : Integer.MAX_VALUE);
    }
    threshold = newThr;
    @SuppressWarnings({"rawtypes","unchecked"})
    //进行创建新的散列表
    Node<K,V>[] newTab = (Node<K,V>[])new Node[newCap];
    table = newTab;
    if (oldTab != null) {
        //把老散列表中的数据添加到新的散列表中
        for (int j = 0; j < oldCap; ++j) {
            Node<K,V> e;
            
            if ((e = oldTab[j]) != null) {
                oldTab[j] = null;
                //判断当前节点是不是属于链表或者红黑树
                if (e.next == null)
                    //当个节点
                    newTab[e.hash & (newCap - 1)] = e;
                else if (e instanceof TreeNode)
                    //红黑树节点
                    ((TreeNode<K,V>)e).split(this, newTab, j, oldCap);
                else { // preserve order
                    //链表节点
                    Node<K,V> loHead = null, loTail = null;
                    Node<K,V> hiHead = null, hiTail = null;
                    Node<K,V> next;
                    do {
                        next = e.next;
                        if ((e.hash & oldCap) == 0) {
                            if (loTail == null)
                                loHead = e;
                            else
                                loTail.next = e;
                            loTail = e;
                        }
                        else {
                            if (hiTail == null)
                                hiHead = e;
                            else
                                hiTail.next = e;
                            hiTail = e;
                        }
                    } while ((e = next) != null);
                    if (loTail != null) {
                        loTail.next = null;
                        newTab[j] = loHead;
                    }
                    if (hiTail != null) {
                        hiTail.next = null;
                        newTab[j + oldCap] = hiHead;
                    }
                }
            }
        }
    }
    //返回扩容后的散列表
    return newTab;
}

```



对上面源码的**总结**：

``` tex
简单的初始化之后，开始进行条件判断
1.oldCap > 0  这个条件意味着什么？
	这个条件说明HashMap已经被初始化过，不是第一次扩容。
	并且散列表的大小大于零，说明不够用了，直接把容量扩大两倍，扩容阈值同样扩大两倍。
	
2.oldCap <= 0 && oldThr > 0 
	oldCap <= 0 and oldThr 说明HashMap已经初始化了，可能是把元素全部删除掉了，它的临界值依旧还是存在的
	
3.oldCap <= 0 && oldThr <= 0
	这个条件说明是第一次扩容，把 newCap 和 newThr 分别赋值为各自的初始值
	newCap = DEFAULT_INITIAL_CAPACITY; ----> 这是初始的数组大小 16
    newThr = (int)(DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY); -----> 初始扩容阈值，初始值为12
```







###### 寻址算法

``` java
static final int hash(Object key) {
    int h;
    return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
    // (h = key.hashCode()) ^ (h >>> 16)这串代码是为了让哈希值更加的均匀。
}
```

**为什么HashMap中的数组长度一定是2的次幂呢?**

- 计算索引时效率更高，如果是2的次幂可以使用与运算代替取模运算。
- 扩容时重新计算索引的效率更高：`hash & oldCap == 0`的元素保留在原地，否则到新位置，`新索引 = 旧索引 + oldCap`



B -> A

e -> A ,next -> B

A

e - > B,next -> A ,

B -> A 

e -> A ,next - > null

A -> B



##### 总结

1. `HashMap`底层原理是哈希表结构，即使用数组和链表或者红黑树
2. 依赖`hashCode`方法和`equals`方法保证键的唯一
3. 如果键存储的是自定义对象，需要重写`hashCode`方法和`equals`方法
4. 如果值存储的是自定义对象，不需要重写`hashCode`方法和`equals`方法



##### `HashMap`中的API

###### `map.computeIfAbsent(参数)`

```java
//.computeIfAbsent(参数);
//源码
default V computeIfAbsent(K key,
        Function<? super K, ? extends V> mappingFunction) {
    	//K是参数类型，V是返回类型
    
    //下面这个方法是判断是不是null的，如果是null就会抛出异常，不是null就会返回本身。
    Objects.requireNonNull(mappingFunction);
    //定义一个变量
    V v;
    
    if ((v = get(key)) == null) {
        //map中不存在key的值
        V newValue;
        if ((newValue = mappingFunction.apply(key)) != null) {
            put(key, newValue);
            return newValue;
        }
    }

    return v;
}
//这里面的mappingFunction可以写成lambda表达式
/*流程：
* 检查 key 是否已经存在于 Map 中。
* 如果 key 存在，直接返回与该 key 相关联的值。
* 如果 key 不存在，调用 mappingFunction 来计算值。
* 将计算出的值与 key 一起插入到 Map 中，并返回这个值。
*/
//总的来说就是返回键值对中值的类型，方法返回的不是 key 的类型，而是与 key 相关联的值（value）的类型
```



###### `map.getOrDefault(参数)`

`Map.getOrDefault(Object key, V defaultValue)`方法的作用是：
  当Map集合中有这个key时，就使用这个key值；
  如果没有就使用默认值defaultValue。



###### `map.merge(key,value,Function)`

merge() 可以这么理解：它将新的值赋值到 key （如果不存在则执行给定的函数处理）或更新给定的key 值对应的 value

**如果key不存在，则 key 的值直接赋值为 value，如果key存在，则按照function函数处理值，function中的参数一就是原值，参数二是value。function函数返回的值就是处理后的值**

**源码**：

```java
default V merge(K key, V value,
        BiFunction<? super V, ? super V, ? extends V> remappingFunction) {
    //判断value和remappingFunction都不为空        
    Objects.requireNonNull(remappingFunction);
    Objects.requireNonNull(value);
    //通过key去获取旧值 若无这个key则null
    V oldValue = get(key);
    //新值 = 旧值为null则新值=null，旧值不为null则新值=  remappingFunction.apply(旧值, 新值);
    V newValue = (oldValue == null) ? value :
               remappingFunction.apply(oldValue, value);
    //判断新值为null的话           
    if(newValue == null) {
        //移除这个key
        remove(key);
    } else {
        //不为null的话，重新put
        put(key, newValue);
    }
    return newValue;
}
```

使用：

```java
//没有使用merge的方法
public static void main(String[] args) {
    ArrayList<Student> students = reStrudents();
    HashMap<String, Integer> stringIntegerHashMap = new HashMap<>();

    students.forEach(student -> {
        if (stringIntegerHashMap.containsKey(student.getName())){
            stringIntegerHashMap.put(student.getName(),
                    stringIntegerHashMap.get(student.getName())+student.getScore());
        }else {
            stringIntegerHashMap.put(student.getName(),student.getScore());
        }});

    System.out.println(stringIntegerHashMap.toString());
}

//使用merge方法
public static void main(String[] args) {
    ArrayList<Student> students = reStrudents();
    HashMap<String, Integer> stringIntegerHashMap = new HashMap<>();
    
    students.forEach(student ->
            stringIntegerHashMap.merge(
                    student.getName(),
                    student.getScore(),
                    Integer::sum
            ));
            
    System.out.println(stringIntegerHashMap.toString());
}
/*
拓展：
	Integer::sum 是一个方法引用（Method Reference），它用于引用已有的方法。
	在这个上下文中，Integer::sum 是一个指向 Integer 类中 sum 静态方法的引用。
	这个方法引用被用作 merge 函数的第三个参数，它定义了当 stringIntegerHashMap 中已经存在一个键时，如何合并这个键对应的值。
*/



map.merge(key, value, (value1, value2) -> value1 - value2);
//这里的value1就是原值，value2就是传进来的value。
```

















##### 练习代码

```java
public static void main(String[] args) {

        String[] str = {"A","B","C","D"};
        //同学们的投票，先设为80个随机值
        Random r = new Random();
        //创建一个集合，存储投票
        ArrayList<String> list = new ArrayList<>();
        for(int i = 0; i < 80; i++){
            int index = r.nextInt(str.length);
            list.add(str[index]);
        }

        //如果统计的东西比较多，不方便使用计数器思想
        //这时可以定义map集合，利用集合进行统计
        HashMap<String, Integer> hm = new HashMap<>();
        for (String name : list){
            boolean flag = hm.containsKey(name);
            if(flag){
                //存在
                Integer i = hm.get(name);
                int count = i + 1;
                hm.put(name,count);

            }else{
                //不存在
                hm.put(name,1);
            }
        }

        System.out.println(hm);

        //求集合中的最大值
        int max = 0;
        Set<Map.Entry<String, Integer>> entries = hm.entrySet();
        for (Map.Entry<String, Integer> entry : entries) {
            if(entry.getValue() > max) max = entry.getValue();
        }

        System.out.println(max);

        //看看谁等于最大值
        for (Map.Entry<String, Integer> entry : entries) {
            if(entry.getValue() == max) System.out.println(entry.getKey());;
        }

    }
```



#### `LinkedHashMap`集合

- 由键决定：有序、不重复、无索引
- 这里的有序指的是保证存储和取出的元素顺序是一样的
- 原理：底层数据结构依然是哈希表，只是每个键值对元素又额外的多了一个双链表的机制记录存储的顺序



###### 源码分析









#### `TreeMap`集合

- `TreeMap`集合和`TreeSet`集合的底层原理一样，都是红黑树结构的
- 由键决定特性：不重复、无索引、可排序
- 可排序：对键进行排序
- ==注意== ： 默认按照键的从小到大进行排序，也可以自己规定键的排序规则

##### 两种排序规则

1. 实现`Comparable`接口，指定比较规则
2. 创建集合的时候传递`Comparator`比较器对象，指定比较规则

其实这里的比较规则和`TreeSet`一样



```java
//创建一个集合
TreeMap<Integer, String> map = new TreeMap<>();

map.put(100,"wuahaha");
map.put(200,"wuahaha");

System.out.println(map);//{100=wuahaha, 200=wuahaha}

TreeMap<student,String> m = new TreeMap<>((o1, o2)-> {
        int i = o1.getAge() - o2.getAge();
        i = i == 0 ? o1.getName().compareTo(o2.getName()) : i;
        return i;
    }
);
student s1 = new student("zhangsan",20);
student s2 = new student("lisi",24);
student s3 = new student("wangwu",27);
student s4 = new student("wangwu",27);

m.put(s1,"江苏");
m.put(s2,"湖南");
m.put(s3,"福建");
m.put(s4,"海南");

System.out.println(m);
//{student{name = zhangsan, age = 20}=江苏, student{name = lisi, age = 24}=湖南, student{name = wangwu, age = 27}=海南}

//根据treeMap的value进行排序


```



##### `TreeMap`源码分析

​	

`TreeMap`集合中每一个存储元素就是一个`Entry`对象

```java
private static final boolean RED   = false;
private static final boolean BLACK = true;

static final class Entry<K,V> implements Map.Entry<K,V> {
    K key;
    V value;
    Entry<K,V> left;
    Entry<K,V> right;
    Entry<K,V> parent;
    boolean color = BLACK;//默认为黑色，后面会进行调整
    
    //......代码省略
    
}
```



在`TreeMap`集合中定义了一个root记录根节点

```java
 private transient Entry<K,V> root;//用来记录根节点
```



`put`源码

```java
public V put(K key, V value) {
	//参数一：键
    //参数二：值
    //参数三：当键重复的时候，是否进行覆盖
    //true，进行覆盖    false,不覆盖
    return put(key, value, true);
}
```



```java
private V put(K key, V value, boolean replaceOld) {
        Entry<K,V> t = root;
    	//获取根节点的地址值，赋值给局部变量t
    	//判断根节点是否为null
    	//如果是null，表示当前是第一次添加元素，会把当前添加的元素当作根节点
    	//如果不是null，表示不是第一次添加元素，直接跳过这个判执行下面的代码
        if (t == null) {
        	//第一次添加元素时，root为空，所以t也被赋值为null
            addEntryToEmptyMap(key, value);
            //添加一个Entry对象到一个空的Map集合当中
            //底层创建了一个entry对象，并赋值给root节点
            return null;
            //返回null表示不用覆盖任何元素
        }
        int cmp;//表示两个元素的键比较后的结果，正数或者负数或者零，用来判断添加在树节点的左边还是右边还是覆盖
        Entry<K,V> parent;//表示当前要添加节点的父节点
        // split comparator and comparable paths
        Comparator<? super K> cpr = comparator;
    	//表示当前的比较规则
    	//如果当前采用默认的自然排序，那么comparator记录的就是null，cpr也是null
    	//如果当前采取比较去排序，那么此时comparator记录的就是比较器
    	
    	//判断当前是否有比较器对象
    	//如果传递了比较器对象，就执行if里面的代码，此时以比较器的规则为准
    	//如果没有传递比较器对象，就执行else里面的代码，此时以自然排序的规则为准
        if (cpr != null) {
            do {
                parent = t;
                cmp = cpr.compare(key, t.key);
                if (cmp < 0)
                    t = t.left;
                else if (cmp > 0)
                    t = t.right;
                else {
                    V oldValue = t.value;
                    if (replaceOld || oldValue == null) {
                        t.value = value;
                    }
                    return oldValue;
                }
            } while (t != null);
        } else {
            /*
            强制类型转换为接口对象时，对象必须实现这个接口或者是其子接口。
            否则，在运行时会抛出ClassCastException异常。
            因为强制类型转换要求被转换的对象必须具备转换后的类型的行为和属性，而这些行为和属性通常由接口定义。
            */
            Comparable<? super K> k = (Comparable<? super K>) key;
            do {
                //把根节点当作当前节点的父节点
                parent = t;
                //调用compareTo方法，比较根节点和当前需要添加节点的大小关系
                cmp = k.compareTo(t.key);
                if (cmp < 0)
                    //负数，继续到根节点的左边去找
                    t = t.left;
                else if (cmp > 0)
                    //正数，到根节点的右边去找
                    t = t.right;
                else {
                    //这里就是为零的情况，判断是否要覆盖
                    V oldValue = t.value;
                    if (replaceOld || oldValue == null) {
                        t.value = value;
                    }
                    return oldValue;
                }
            } while (t != null);
        }
    	//把当前节点按照指定规则进行添加
        addEntry(key, value, parent, cmp < 0);
        return null;
    }
```



```java
private void addEntry(K key, V value, Entry<K, V> parent, boolean addToLeft) {
        Entry<K,V> e = new Entry<>(key, value, parent);
        if (addToLeft)
            parent.left = e;
        else
            parent.right = e;
    	//添加完毕之后按照红黑规则进行调整
        fixAfterInsertion(e);
        size++;
        modCount++;
    }

```





```java
private void fixAfterInsertion(Entry<K,V> x) {
        x.color = RED;//因为红黑树默认节点为红色
		//按照红黑规则进行调整
    
    	//parantOf获取X的父节点
    	//parantOf（parantOf（x））获取x的爷爷节点
    	//leftOf获取x的左子节点
        while (x != null && x != root && x.parent.color == RED) {
            //判断当前父节点是爷爷节点的左子节点还是右子节点
            //目的：获取当前节点的叔叔节点
            if (parentOf(x) == leftOf(parentOf(parentOf(x)))) {
                //当前节点的父节点是爷爷节点的左子节点
                //下面这个y就是用来记录叔叔节点的
                Entry<K,V> y = rightOf(parentOf(parentOf(x)));
                if (colorOf(y) == RED) {
                    //当前节点的叔叔节点是红色
                    setColor(parentOf(x), BLACK);//把父节点设置为黑色
                    setColor(y, BLACK);//把叔叔节点设置为黑色
                    setColor(parentOf(parentOf(x)), RED);//把爷爷节点设置为红色
                    x = parentOf(parentOf(x));//把爷爷节点设置为当前节点
                } else {
                    //当前节点的叔叔节点是黑色
                    if (x == rightOf(parentOf(x))) {
                        x = parentOf(x);
                        rotateLeft(x);//左旋
                    }
                    setColor(parentOf(x), BLACK);
                    setColor(parentOf(parentOf(x)), RED);
                    rotateRight(parentOf(parentOf(x)));
                }
            } else {
                //当前节点的父节点是爷爷节点的右子节点
                Entry<K,V> y = leftOf(parentOf(parentOf(x)));
                if (colorOf(y) == RED) {
                    setColor(parentOf(x), BLACK);
                    setColor(y, BLACK);
                    setColor(parentOf(parentOf(x)), RED);
                    x = parentOf(parentOf(x));
                } else {
                    if (x == leftOf(parentOf(x))) {
                        x = parentOf(x);
                        rotateRight(x);
                    }
                    setColor(parentOf(x), BLACK);
                    setColor(parentOf(parentOf(x)), RED);
                    rotateLeft(parentOf(parentOf(x)));
                }
            }
        }
        root.color = BLACK;
    }
```



###### 思考题目

1. `TreeMap`集合添加元素时，键是否需要重写`HashCode`方法和`equals`方法？

   不需要重写`HashCode`方法和`equals`方法，因为`TreeMap`集合在添加元素时不是依靠键算出哈希值找到键值对对象存放位置的

2. `HashMap`是由哈希表构成的，JDK8开始由数组、链表、红黑树组成，既然有了红黑树，是否需要利用`comparable`指定排序规则？是否需要传递比较器`comparator`指定比较规则？

   都是不需要的，在`HashMap`底层默认是利用哈希值的大小关系来创建红黑树的

3. `TreeMap`和`HashMap`谁的效率更高？

   如果是最坏的情况，添加了8个元素，这8个元素形成了链表，此时`TreeMap`的效率更高，但是这种情况出现的机率非常小

   一般而言，还是`HashMap`效率更高

4. 你觉得在`Map`集合中，java会提供一个如果键重复了，不会覆盖的`put`方法吗？

   会，有这个方法。`putIfAbsent`方法，但是这个方法本身不重要

   传递一个思想：

   代码中的逻辑都有两面性，如果我么知道了其中的A面，而且代码中还发现由变量可以控制两面性，那么该逻辑一定会有B面

   习惯：

   `boolean`类型的变量控制，一般只有AB两面，因为`boolean`只有两个值

   int类型的变量控制，一般至少会有三面，因为int可以取多个值。

5. 三种双列集合该怎么选择？

   `HashMap`、`LinkedHashMap`、`TreeMap`三种双列集合

   默认：`HashMap`（效率最高）

   如果要保证存取有序：`LinkedHashMap`

   如果要进行排序：`TreeMap`



#### `properties`集合

`properties`是一个双列集合集合，拥有Map集合所有的特点

重点：有一些特有的方法，可以把集合中的数据，按照键值对的形式写到配置文件中，也可以把配置文件中数据，读取到集合中来

```java
Properties prop = new Properties();
try {
    prop.load(new FileReader("PuzzleGame\\src\\game.properties"));
} catch (IOException ex) {
    throw new RuntimeException(ex);
}
String path = (String)prop.get("account");


//还有写的方法
prop.store(OutputStream);

```







### Map中遍历方式

#### 1.键找值

```java
Map<String,String> m = new HashMap<>();
m.put("郭靖","黄蓉");
m.put("韦小宝","沐剑屏");
m.put("尹志平","小龙女");

//Map的第一种遍历方式，键找值方式
//获取所有的键，把这些键放到一个单列集合（Set）中去
Set<String> keys = m.keySet();

//遍历单列集合，得到每一个键
//增强for形式
for (String key : keys) {
    String value = m.get(key);//get是通过键返回值
    System.out.println(key + " = " + value);
}
System.out.println("-------------------------------");

//迭代器方法遍历
Iterator<String> iterator = keys.iterator();
while(iterator.hasNext()){
    String key = iterator.next();
    String value = m.get(key);
    System.out.println(key + " = " + value);
}
System.out.println("--------------------------------");

//lambda遍历
keys.forEach(key->{
        String value = m.get(key);
        System.out.println(key + " = " + value);
    }
);
```



#### 2.键值对



```java
      Map<String,String> m = new HashMap<>();
        m.put("郭靖","黄蓉");
        m.put("韦小宝","沐剑屏");
        m.put("尹志平","小龙女");


        Set<Map.Entry<String, String>> entries = m.entrySet();//获得键值对的对象
        //Entry是Map中的一个内部接口

        //增强for
        for (Map.Entry<String, String> entry : entries) {
            System.out.println(entry.getKey() + " = " + entry.getValue());
        }
        System.out.println("-----------------------------------");

        //迭代器遍历
        Iterator<Map.Entry<String, String>> it = entries.iterator();
        while(it.hasNext()){
            Map.Entry<String, String> next = it.next();
            System.out.println(next.getKey() + " = " + next.getValue());
        }

        System.out.println("-------------------------------------");
        //lambda表达式
        entries.forEach(stringStringEntry->System.out.println(stringStringEntry.getKey() + " = " + stringStringEntry.getValue()));


```



自己的理解：

`Comsumer`接口只有一个泛型，类型为调用集合里面存放元素的类型

`BigComsumer`接口有两个泛型，类型为调用集合里面存放元素的类型





#### 3.`lambda`表达式



```java
 Map<String,String> m = new HashMap<>();
        m.put("郭靖","黄蓉");
        m.put("韦小宝","沐剑屏");
        m.put("尹志平","小龙女");

        m.forEach(new BiConsumer<String, String>() {
            @Override
            public void accept(String key, String value) {
                System.out.println(key + "->" + value);
            }
        });

        System.out.println("-----------------------");

        m.forEach((key, value)-> System.out.println(key + "->" + value));
```





## 可变参数



作用 ------>在形参中接收多个数据

### 格式

属性类型...变量名  ---- （int...`args`）

### 底层

底层可变参数就是一个数组，只不过不需要我们自己创建，java已经帮我们创建好了

### 细节

1. 在方法的形参中最多只能写一个可变参数

   可变参数可以理解为一个大胖子，有多少吃多少，如果以传一堆数据过来，哪一些是第一个可变参数中的，哪些是第二个可变参数中的呢？是不知道的

2. 在方法中如果除了可变参数外还有其他的形参，可变参数要放在最后

```java
public static int getSum(int a, int...args);
```





## `Collections`工具类

作用：`Collections`不是集合，而是集合的工具类



Collections常用的API

| 方法名称                                                     | 说明                                  |
| ------------------------------------------------------------ | ------------------------------------- |
| `public static <T> boolean addAlll(Collection  <T> c,T...elements)` | 批量添加元素，只能给单列集合批量添加  |
| `public static void shuffle (List<?> list)`                  | 打乱List集合元素的顺序，不能传Set集合 |



`emptyList();`

其他的可以去API帮助文档查看





## 创建不可变集合

不可变集合：不可以被修改的集合，长度不可以修改，内容也不可以修改



### 创建不可变集合的应用场景

- 如果某个数据不能被修改，把它防御性地拷贝到不可变集合中是个很好的实践。
- 当集合对象被不可信的库调用时，不可变形式是安全的

简单理解就是不想被别人修改集合中的内容



### 创建不可变集合的书写格式

在List、Set、Map接口中，都存在静态的of方法，都可以获取一个不可变的集合

| 方法名称                               | 说明                               |
| -------------------------------------- | ---------------------------------- |
| `static <E> List<E> of(E...elements)`  | 创建一个具有指定元素的List集合对象 |
| `static <E> Set<E> of(E...elements)`   | 创建一个具有指定元素的Set集合对象  |
| `static <E> Map<E,V> of(E...elements)` | 创建一个具有指定元素的Map集合对象  |

==注意== ： 这个创建出来的集合不能添加、不能删除、不能修改。



### 细节 

- 当要获取一个不可变的Set集合时，要保证里面的元素唯一不能有重复的，有重复的会报错
- 获取一个不可变的Map集合，要保证键唯一
- 在不可变的Map集合中的of方法，参数是有上限的，最多只能传递20个参数，即10个键值对，而不可变的List和Set的集合没有上限，接口中有可变参数形式的方法，在Map接口中没有可变参数的方法，最大的是传递是个键值对的方法。（想一想，如果要设计一个可变参数的Map集合，是需要两个可变参数的，一个是用来记录键的可变参数，另一个是用来记录值的可变参数，可是一个方法中最多只能有一个可变参数，不能实现有两个可变参数分别记录键和值）

```java
public static <E> Map<E,V> (E...key,V...value);
//注意，这是错误的！！！！
//如果要实现Map的不可变集合，就要有两个可变参数，像上面方法中写的一样，你传一堆数据过去会被认为全部是键，因为E...key在前面，后面的E...value分配不到数据，java会认为传过去的数据全部都是键-key
```

- 如果需要传递的参数大于是个键值对，则需要使用Map接口中的另外一个方法-->`ofEntries`

  ```java
  static <K, V> Map<K, V> ofEntries(Entry<? extends K, ? extends V>... entries){
      //idea中的源码
  }
  //创建一个Map集合，往里面添加键值对
  //把这个集合用toArray的带参数方法去转化为数组
  //再把数组用ofEntries方法转化为不可变集合
  ```

  先创建一个Map集合（例如HashMap），添加一些键值对元素，然后使用`Map.copyOf()`方法，就会返回一个不可变的Map集合

  ```java
  //JDK10才开始有的，如果是JDK10以前的版本就需要使用原始的方法ofEnrtyies()
  //先创建一个Map集合，往里面添加键值对
  //再使用Map.copyOf(放刚创建的添加了键值对的Map集合)就可以返回一个不可变集合
  static <K, V> Map<K, V> copyOf(Map<? extends K, ? extends V> map) {
          if (map instanceof ImmutableCollections.AbstractImmutableMap) {
              return (Map<K,V>)map;
          } else if (map.isEmpty()) { // Implicit nullcheck of map
              return Map.of();
          } else {
              return (Map<K,V>)Map.ofEntries(map.entrySet().toArray(new Entry[0]));
          }
      }
  ```

  



## stream流

### stream流的作用

结合lambda表达式，简化集合、数组的操作



### stream流的使用步骤

1. 先得到一条stream流(流水线)，并把数据放上去

   | 获取方式     | 方法名                                          | 说明                     |
   | ------------ | ----------------------------------------------- | ------------------------ |
   | 单列集合     | `default Stream<E> stream()`                    | Collection中的默认方法   |
   | 双列集合     | 无                                              | 无法直接使用stream流     |
   | 数组         | `public static <T> Stream<T> stream(T[] array)` | Arrays工具类中的静态方法 |
   | 一堆零散数据 | `public static <T> Stream<T> of(T...value)`     | `Stream`接口中的静态方法 |

   

2. 利用stream流中的各种API进行操作

   这些API中又可以分为中间方法和终结方法

   - 中间方法：方法调用完后还可以调用其他方法（过滤、转化等），会返回新的stream流，原来的stream流只能使用一次，建议使用链式编程

     | 名称                                              | 说明                                                         |
     | ------------------------------------------------- | ------------------------------------------------------------ |
     | `Stream<T> filter(Predicate<? super T) predicate` | 过滤                                                         |
     | `Stream<T> limit(long maxSize)`                   | 获取前几个元素                                               |
     | `Stream<T> skip(long n)`                          | 跳过前几个元素                                               |
     | `Stream<T> distinct()`                            | 元素去重，依赖`hashCode`和`equals`方法，自定义对象需要重写`hashCode`方法和`equals`方法 |
     | `static <T> Stream<T> concat(Stream a,Stream b)`  | 合并a和b两个流为一个流                                       |
     | `Stream<R> map(Function<T,R> mapper)`             | 转换流中的数据类型                                           |

     

     ```java
     ArrayList<String> list = new ArrayList<>();
     Collections.addAll(list,"张三","李四","王五","赵六","钱七","狂铁");
     //过滤
     list.stream().filter(string->string.startsWith("张")).forEach(System.out::println);//张三
     System.out.println("---------------------");
     //获取前几个元素
     list.stream().limit(3).forEach(s->System.out.println(s));//张三 李四 王五
     System.out.println("-------------------------");
     //跳过前几个元素
     list.stream().skip(3).forEach(s-> System.out.println(s));//赵六 钱七 狂铁
     System.out.println("---------------------------");
     //元素去重
     ArrayList<String> list01 = new ArrayList<>();
     Collections.addAll(list01,"张三","张三","张三","李四");
     list01.stream().distinct().forEach(s->System.out.println(s));//张三 李四
     System.out.println("--------------------------");
     //把两个流合并为一个流
     Stream.concat(list.stream(),list01.stream()).forEach(s-> System.out.println(s));
     //张三 李四 王五 赵六 钱七 狂铁 张三 张三 张三 李四
     System.out.println("------------------------");
     //转化流中的数据类型
     ArrayList<String> list02 = new ArrayList<>();
     Collections.addAll(list02,"张三-1","李四-2","王五-3");
     list02.stream()
             .map(s->Integer.parseInt(s.split("-")[1]))
             .forEach(s-> System.out.println(s));//1 2 3
     ```

   

   


   - **终结方法**：方法调用完后不能再调用其他方法(统计、打印等)

     | 方法                            | 说明                                                         |
     | ------------------------------- | ------------------------------------------------------------ |
     | `void forEach(Consumer action)` | 遍历，返回值是void，也就说明是最后一步，里面的操作会影响原集合的内容 |
     | `long count()`                  | 统计                                                         |
     | `toArray()`                     | 收集流中的数据。放到数组中                                   |
     | `collect(Collector collector)`  | 收集流中的数据，放到集合中，放到Set集合中时流中的元素可以有重复，<br />但是放到Map集合中时流中元素(安排为键的部分)不能重复，否则会报错 |

     

     ```java
     long count = list.stream().count();
     System.out.println(count);//6
     ```

     

     **方法解释：**
     
     ```java
     //1.
     //toArray有两种方法，一种是有参的，一种是无参的
     //无参的是直接返回Object类型的数组
     //有参的是返回指定类型的数组
     
     //IntFunction的泛型：具体类型的数组
     //apply的形参：流中的数据个数，要跟数组的长度保持一致
     //apply方法的返回值：是一个装着流里面所有数据的数组
     //toArray方法的参数作用：负责创建一个指定类型的数组
     //toArray方法的底层：会得到流里面的每一个数据，并把数据放到数组中
     //toArray方法的返回值：是一个装有流里面所有数据的数组
     String[] arr = list.stream().toArray(new IntFunction<String[]>() {
         @Override
         public String[] apply(int value) {
             return new String[value];
         }
     });
     
     for(String str : arr){
         System.out.print(str + " ");
     }
     //张三 李四 王五 赵六 钱七 狂铁
     //-------------------------------------
     String[] arr = list.stream().toArray(value -> new String[value]);
     for(String str : arr){
         System.out.print(str + " ");
     }
     //张三 李四 王五 赵六 钱七 狂铁
     
     //2.
     //colletc方法
     //注意 collect 方法里面的接收参数是Collector类型
     //一般传参数都是使用Collectors工具类，里面有很多方法，常用的就是toList()、toSet()、toMap()
     
     ....collector(Collectors.toList());
     ....collector(Collectors.toSet());//里面元素会去重
     ....collector(Collectors.toMap());//
     
     //源码
     Collector<T, ?, Map<K,U>> toMap(Function<? super T, ? extends K> keyMapper,
                                         Function<? super T, ? extends U> valueMapper) {
             return new CollectorImpl<>(HashMap::new,
                                        uniqKeysMapAccumulator(keyMapper, valueMapper),
                                        uniqKeysMapMerger(),
                                        CH_ID);
         }
     
     //toMap：
     //参数一：表示键的生成规则
     //参数二：表示值的生成规则，参数二有时会使用Function.identity()方法。这个方法是 Java 8 中 java.util.function.Function 接口的一个静态方法。它的作用是返回一个恒等函数（Identity Function），即输入什么值，就返回什么值，不做任何转换或处理。
     //代码如下
     static <T> Function<T, T> identity()
     
     /*参数一：
     	Function的两个泛型
     		泛型一：表示流中的每一个数据的类型
     		泛型二：表示Map集合中键的数据类型
     	
     	apply方法
     		形参：依次表示流里面每个数据
     		方法体：生成键的代码
     		返回值：已经生成的键
     		
     参数二：
     	Function的两个泛型
     		泛型一：表示流中的每一个数据的类型
     		泛型二：表示Map集合中值的数据类型
     	
     	apply方法
     		形参：依次表示流里面每个数据
     		方法体：生成值的代码
     		返回值：已经生成的值
     	
     */
     
     //关于Colletors工具类的疑问：为什么在collect方法里面作为参数可以获取执行collet方法的流中的数据？
     //Collectors 工具类本身并不直接获取流的信息，而是通过定义一个 Collector 接口的实现来指导流的收集过程。Collector 接口定义了如何将流中的元素逐步累积到一个结果容器中。
     //就拿上面的toMap方法解释，使用Collectors.toMap()方法，它会返回一个Collector实例对象，这个实例对象在调用toMap方法时设定如何从流中收集数据到Map集合中，就是说只是设定了怎么处理流中的数据，而不是返回处理好的结果。
     //大概流程就是，Collectors.toMap()设定了流在把数据收集到Map中的条件，执行collect方法时就会遵守这个设定，按照toMap中参数一的函数设置map集合的key，按照参数二的函数设置map集合的key。
     
     
     ```
     



####  `collect`方法

**`collect()` 就是把流式处理完的数据，“收集”成你想要的集合（List、Set、Map 等）。**Stream 流本身**只是数据管道，不存数据**，处理完必须用 `collect()` 转成真正能用的集合。

核心作用（超通俗） - 流处理完 → **不是正常集合，不能直接用** - `collect(收集器)` → **把流转成 List / Set / Map / 其他类型** - 它是**流的“出口”**，没有它，流处理完就没了 

​	最常见用法（你刚才代码就在用这个） 

``` java
Set<Integer> set = Arrays.stream(nums).boxed().collect(Collectors.toCollection(TreeSet::new));
/**
👉 这里 `collect()` 的作用： 

1. 接收前面处理好的 `Integer` 流 
2. 按照指定规则（`TreeSet`）收集起来 
3.  **返回一个 TreeSet 集合**给你用
*/
```



​	3 个最常用模板（背会就够用）  
​	① 收集成 List ```java List<Integer> list = stream.collect(Collectors.toList()); ``` <br/>	② 收集成 Set（自动去重） ```java Set<Integer> set = stream.collect(Collectors.toSet()); ```
​	③ 收集成 TreeSet（有序+去重） ```java TreeSet<Integer> treeSet = stream.collect(Collectors.toCollection(TreeSet::new)); ```

​	

**Collectors类的方法**

**`toSet()`**：固定返回 **`HashSet`**（无序）

**`toList()`**：固定返回 **`ArrayList`**

**`toCollection(集合::new)`**：你指定返回 **`TreeSet` / `LinkedList` / 自定义集合**









### 总结

1. `Stream`流的作用

   结合了Lambda表达式，简化集合、数组的操作

2. `Stream`的使用步骤

   - 获取`Stream`流对象
   - 使用中间方法处理数据
   - 使用终结方法处理数据

3. 如何获取`Stream`流对象

   - 单列集合：`Collection`中默认的方法`stream`
   - 双列集合：不能直接获取
   - 数组：`Arrays`工具类中的静态方法`stream`
   - 一堆零散的数据（同类型的数据）：`Stream`接口中的静态方法`of`

4. 常见方法

   - 中间方法：`filter`,`limit`,`skip`,`distinct`,`concat`,`map`
   - 终结方法：`forEach`,`count`,`collect`



### 代码练习

1. 添加一些整数在集合中，过滤奇数，留下偶数，并保留起来

   ```java
   ArrayList<Integer> list = new ArrayList<>();
   Collections.addAll(list,1,2,3,4,5,6,7,8,9,10);
   
   List<Integer> newList = list.stream().filter(number -> number % 2 == 0).collect(Collectors.toList());
   
   System.out.println(newList);//[2, 4, 6, 8, 10]
   ```

2. 创建一个`ArrayList`集合，添加字符串，字符串前面是姓名，后面是年龄，保留年龄大于24的人，并将结果收集到Map集合中，姓名为键，年龄为值。

   ```java
   ArrayList<String> list = new ArrayList<>();
   Collections.addAll(list,"张三,23","李四,24","王五,25");
   
   Map<String, Integer> map = list.stream()
                       .filter(s -> Integer.parseInt(s.split(",")[1]) >= 24)
                       .collect(Collectors.toMap(s -> s.split(",")[0], s -> Integer.parseInt(s.split(",")[1])));
   
   System.out.println(map);
   //{李四=24, 王五=25}
   ```

3. ```java
   //现在有两个ArrayList集合，分别存储6名男演员和6名女演员的名字和年龄
   //姓名和年龄之间用逗号隔开
   //1.男演员只要名字为三个字的两个人
   //2.女演员只要姓杨的，并且不要第一个姓杨的
   //3.把过滤后的男演员和女演员姓名合并到一起
   //4.将上一步的演员封装成Actor对象
   //5.将所有的演员对象都保留在ArrayList集合中
   
   ArrayList<String> list1 = new ArrayList<>();
   ArrayList<String> list2 = new ArrayList<>();
   Collections.addAll(list1,"蔡坤坤,24","叶齁咸,23","刘不甜,22","吴签,24","谷嘉,30","肖梁梁,27");
   Collections.addAll(list2,"赵小颖,35","杨颖,36","高元元,43","张天天,31","刘诗,35","杨小幂,33");
   
   List<Actor> newList = Stream.concat(list1.stream().filter(s -> s.split(",")[0].length() == 3).limit(2)
                   , list2.stream().filter(s -> s.split(",")[0].startsWith("杨")).skip(1))
           .map(s -> new Actor(s.split(",")[0], Integer.parseInt(s.split(",")[1])))
           .collect(Collectors.toList());
   
   for(Actor actor : newList){
       System.out.println(actor);
   }
   //Actor{name = 蔡坤坤, age = 24}
   //Actor{name = 叶齁咸, age = 23}
   //Actor{name = 杨小幂, age = 33}
   ```

   



## 方法引用



把已经有的方法拿过来用，当作函数式接口中抽象方法的方法体



不是所有的方法都可以被引用，需要有下面的条件

1. 引用处必须是函数式接口
2. 被引用的方法（可以是java写的，也可以是一些第三方的工具类，或者自己写的方法）必须已经存在
3. 被引用的方法的形参和返回值需要和抽象方法保持一致
4. 被引用的方法的功能要满足当前需求



### 代码引入

```java
public class text {
    public static void main(String[] args) {
        //创建一个数组，进行倒序排列
        Integer[] arr = {3, 5, 4, 1, 6, 2};
        //匿名内部类
        Arrays.sort(arr, new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return o2 - o1;
            }
        });

        //lambda表达式
        Arrays.sort(arr,(Integer o1,Integer o2) -> {
                return o2 - o1;
        });

        //lambda表达式简化格式
        Arrays.sort(arr,(o1,o2)-> o2 - o1);

        //方法引用
        //表示引用text类里面的subtraction方法
        //把这个方法当作抽象方法的方法体
        Arrays.sort(arr,text::subtraction);

        System.out.println(Arrays.toString(arr));
		//[6, 5, 4, 3, 2, 1]
    }

    //方法引用需要使用到的方法
    public static int subtraction(int num1, int num2){
        return num2 - num1;
    }
}

```



### 一些问题

1. 什么是方法引用？

   把已经存在的方法拿过来使用，当作函数式接口中抽象方法的方法体

2. “：：" 是什么符号?

   方法引用符

3. 方法引用时需要注意什么？

   - 需要有函数式接口
   - 被引用方法必须已经存在
   - 被引用方法的形参和返回值需要和抽象方法保持一致
   - 被引用方法的功能要满足当前的需求



### 方法引用的分类



#### 1.引用静态方法

##### 格式

类名::静态方法(`Integer::parseInt`)

```java
//转成int
ArrayList<String> list = new ArrayList<>();
Collections.addAll(list,"1","2","3","4","5","6");

list.stream().map(s-> Integer.parseInt(s)).forEach(s-> System.out.println(s));

list.stream().map(Integer::parseInt).forEach(System.out::println);

```





#### 2.引用成员方法

##### 格式：

 对象::成员方法



##### I、引用其他类的成员方法

###### 格式

其他类对象::方法名

```java
//转成int
ArrayList<String> list = new ArrayList<>();
Collections.addAll(list,"张无忌","周芷若","赵敏","张强","张三丰");

//   list.stream().filter(s->s.startsWith("张") && s.length() == 3).forEach(s-> System.out.println(s));

list.stream().filter(new Predicate<String>() {
    @Override
    public boolean test(String s) {
        return s.startsWith("张") && s.length() == 3;
    }
}).forEach(s->System.out.println(s));

list.stream().filter(new stringOperation()::text1).forEach(s->System.out.println(s));


//下面是另外一个类

public class stringOperation{
    public boolean text1(String s){
        return s.startsWith("张") && s.length() == 3;
    }
}

```



##### II、引用本类的成员方法

###### 格式

this::方法名（引用处不能是静态方法，静态方法没有`this`关键字）





##### III、引用父类的成员方法

###### 格式

super::方法名（引用处不能是静态方法）





#### 3.引用构造方法

##### 格式

类名::new(Student::new)





#### 4.其他调用方式



##### I、使用类名引用成员方法

格式

类名::成员方法（String::substring）



该方法引用的规则：

1. 需要有函数式接口
2. 被引用的方法必须已经存在
3. 被引用方法的形参，需要和抽象方法的第二个形参到最后一个形参保持一致，返回值需要保持一致
4. 被引用的方法的功能需要满足当前的需求



抽象方法形参的详解：

- 第一个参数：表示被引用方法的调用者，决定了可以引用哪些类中的方法（只能引用调用者类中的方法）

  ​					 在`Stream`流中，第一个参数一般都可以表示流里面的每一个数据

  ​					 假设流里面的数据是字符串，那么使用这种方式进行方法引用，只能引用`String`这个类中的方法

- 第二个参数到最后一个参数：跟被引用方法的形参保持一致，如果没有第二个参数，说明被引用的方法需要的是无参的成员方法



###### 局限性

不能引用所有类中的成员方法，是跟抽象方法的第一个参数有关，这个参数是什么类型的，那么就只能引用这个类中的方法



```java
ArrayList<String> list = new ArrayList<>();
Collections.addAll(list,"aaa","bbb","ccc","ddd");

list.stream().map(new Function<String, String>() {
    @Override
    public String apply(String s) {
        return s.toUpperCase();
    }
}).forEach(s-> System.out.println(s));

System.out.println("-------------------");

//拿着流里面的每一个数据，去调用String类里面的toUpperCase方法，方法的返回值就是转化之后的结果
list.stream().map(String::toUpperCase).forEach(System.out::println);
```



##### II、引用数组的构造方法

格式

数据类型[]::new

范例：int[]::new



数组的类型需要和流中的数据类型一致





### 代码练习

```java
ArrayList<String> list = new ArrayList<>();
Collections.addAll(list,"zhangsan,23","lisi,25","wangwu,26");

List<student> newList = list.stream()
        .map(s-> new student(s.split(",")[0],Integer.parseInt(s.split(",")[1])))
        .toList();

String[] str = newList.stream().map(student::getName).toArray(String[]::new);

for(String s : str) {
    System.out.println(s);
}
```



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



