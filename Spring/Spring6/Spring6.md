



# Spring6

语雀讲义地址：https://www.yuque.com/dujubin/ltckqu/kipzgd?#Aas7m



## 什么是Spring？

Spring 是一个轻量级开源框架，核心是 IoC 和 AOP，用于解耦代码、管理对象和实现企业级功能。

**Spring 是一个“技术生态/体系”**，不只是 Spring FrameWork。

**Spring FrameWork 是 Spring的核心框架**



Spring FrameWork是所有Spring技术的基础，提供三大核心能力：IoC、DI、AOP

Spring 是一个完整的生态体系，除了核心的 Spring Framework 外，还包括 Spring Boot、Spring MVC、Spring Cloud、Spring Security、Spring Data 等多个子项目，分别用于快速开发、Web、微服务、安全和数据访问等场景。



### 使用Spring的好处

从Spring 框架的**特性**来看：

- 非侵入式：基于Spring开发的应用中的对象可以不依赖于Spring的API（写代码的时候是不是没有导入过包`org.springframework.stereotype.Service;`）
- 控制反转：IOC——Inversion of Control，指的是将对象的创建权交给 Spring 去创建。使用 Spring 之前，对象的创建都是由我们自己在代码中new创建。而使用 Spring 之后。对象的创建都是给了 Spring 框架。
- 依赖注入：DI——Dependency Injection，是指依赖的对象不需要手动调用 setXX 方法去设置，而是通过配置赋值。
- 面向切面编程：Aspect Oriented Programming——AOP
- 容器：Spring 是一个容器，因为它包含并且管理应用对象的生命周期
- 组件化：Spring 实现了使用简单的组件配置组合成一个复杂的应用。在 Spring 中可以使用XML和Java注解组合这些对象。
- 一站式：在 IOC 和 AOP 的基础上可以整合各种企业应用的开源框架和优秀的第三方类库（实际上 Spring 自身也提供了表现层的 SpringMVC 和持久层的 Spring JDBC）

从使用Spring 框架的**好处**看：

- Spring 可以使开发人员使用 POJOs 开发企业级的应用程序。只使用 POJOs 的好处是你不需要一个 EJB 容器产品，比如一个应用程序服务器，但是你可以选择使用一个健壮的 servlet 容器，比如 Tomcat 或者一些商业产品。
- Spring 在一个单元模式中是有组织的。即使包和类的数量非常大，你只要担心你需要的，而其它的就可以忽略了。
- Spring 不会让你白费力气做重复工作，它真正的利用了一些现有的技术，像 ORM 框架、日志框架、JEE、Quartz 和 JDK 计时器，其他视图技术。
- 测试一个用 Spring 编写的应用程序很容易，因为环境相关的代码被移动到这个框架中。此外，通过使用 JavaBean-style POJOs，它在使用依赖注入注入测试数据时变得更容易。
- Spring 的 web 框架是一个设计良好的 web MVC 框架，它为比如 Structs 或者其他工程上的或者不怎么受欢迎的 web 框架提供了一个很好的供替代的选择。MVC 模式导致应用程序的不同方面(输入逻辑，业务逻辑和UI逻辑)分离，同时提供这些元素之间的松散耦合。模型(Model)封装了应用程序数据，通常它们将由 POJO 类组成。视图(View)负责渲染模型数据，一般来说它生成客户端浏览器可以解释 HTML 输出。控制器(Controller)负责处理用户请求并构建适当的模型，并将其传递给视图进行渲染。
- Spring 对 JavaEE 开发中非常难用的一些 API（JDBC、JavaMail、远程调用等），都提供了封装，使这些API应用难度大大降低。
- 轻量级的 IOC 容器往往是轻量级的，例如，特别是当与 EJB 容器相比的时候。这有利于在内存和 CPU 资源有限的计算机上开发和部署应用程序。
- Spring 提供了一致的事务管理接口，可向下扩展到（使用一个单一的数据库，例如）本地事务并扩展到全局事务（例如，使用 JTA）



-----------



## 什么是OCP

> OCP是软件七大开发原则当中最基本的一个原则：开闭原则（Open-Close Principle）
>
> 对什么开？对扩展开（open）
>
> 对什么闭？对修改闭（close）
>
> OCP开闭原则最核心的内容是什么？
>
> 只要在扩展系统功能的时候，没有修改以前的代码就是符合OCP开闭原则，反之，如果在扩展系统功能的时候修改了代码那么这个设计就是失败的，违背OCP开闭原则。
>
> OCP原则是最核心的，最基本的，其他的六个原则都是为这个原则服务的



---------



## 依赖倒置原则 (DIP原则)

> * 什么是依赖倒置原则？
>
>    面向接口编程、面向抽象编程，不要面向具体编程，全称为：Dependency Inversion Principle
>
> * 依赖倒置的目的？
>
>   降低程序的耦合度，提高扩展力。
>
> * 什么叫做违背依赖倒置原则？
>
>   上依赖下，就是违背，只要“下”一改动，“上”就受到牵连。
>
> * 什么叫做符合依赖倒置原则？
>
>   上不依赖下。



---------



## 控制反转-IoC（Inversion of Control）

> 控制反转是一种编程思想，或者叫是一种新型的设计模式
>
> 反转的是两件事：
>
> 1. 不在程序中采用硬编码的方式来new对象了（new对象我不管了，new对象的权力交出去了）
> 2. 不在程序中采用硬编码的方式来维护对象的关系了（对象之间的维护权我也不管了，也交出去了）
>
> **这里的关系是开发人员和框架之间的，控制反转也是在这二者之间反转，使用Spring之前，对象、对象关系的控制权都在开发人员手中，但是使用了Spring之后，对象、对象关系就不由开发人员控制了，而是交付出去，给框架进行控制。**
>
> 其中一种控制反转的实现方式就是依赖注入（Dependency Injection，简称DI）。
>
> 依赖注入可通过set注入（执行set方法给属性赋值）和构造方法注入（执行构造方法给属性赋值）



### IoC提问

Spring框架管理这些Bean的创建工作，即由用户管理Bean转变为框架管理Bean，这个就叫**控制反转 - Inversion of Control (IoC)**

Spring 框架托管创建的Bean放在哪里呢？ 这便是**IoC Container**;

Spring 框架为了更好让用户配置Bean，必然会引入**不同方式来配置Bean？ 这便是xml配置，Java配置，注解配置**等支持

Spring 框架既然接管了Bean的生成，必然需要**管理整个Bean的生命周期**等；

应用程序代码从Ioc Container中获取依赖的Bean，注入到应用程序中，这个过程叫 **依赖注入(Dependency Injection，DI)** ； 所以说控制反转是通过依赖注入实现的，其实它们是同一个概念的不同角度描述。通俗来说就是**IoC是设计思想，DI是实现方式**
**DI 不是应用程序主动从 IoC 容器获取对象，而是 IoC 容器在对象创建过程中，将其依赖的对象自动注入进去，使应用程序不再关心依赖的创建和获取。**

在依赖注入时，有哪些方式呢？这就是构造器方式，@Autowired, @Resource, @Qualifier... 同时Bean之间存在依赖（可能存在先后顺序问题，以及**循环依赖问题**等）



----------



## **Spring容器启动时会进行的操作**



1. **解析XML配置文件**：Spring容器会读取XML配置文件，并识别出所有的`<bean>`标签。
2. **注册Bean定义**：对于每个`<bean>`标签，Spring容器会创建一个`BeanDefinition`对象，这个对象包含了bean的类信息、作用域、生命周期回调、属性值等元数据。这些`BeanDefinition`对象会被注册到Spring容器的内部数据结构中，以便后续使用。
3. **创建Bean实例**：对于非懒加载（`lazy-init="false"`）的`singleton`作用域的bean，Spring容器会在启动时预实例化这些bean。这意味着Spring会使用bean的构造函数或工厂方法创建bean的实例。
4. **属性填充**：==在bean实例化之后==，Spring容器会根据`<property>`标签中定义的属性值，使用setter方法（或其他注入方式，如构造函数注入或字段注入）来设置bean的属性。
5. **依赖注入**：如果bean有依赖其他bean，Spring容器会解析这些依赖关系，并注入相应的bean实例。
6. **初始化回调**：对于`singleton`作用域的bean，如果定义了`init-method`，Spring容器会在属性填充和依赖注入之后调用这个初始化方法。
7. **后处理**：Spring容器可能会对bean进行后处理，例如应用`@PostConstruct`注解的方法。



spring的8大模块

![image-20241024083546511](C:\Users\heban\AppData\Roaming\Typora\typora-user-images\image-20241024083546511.png)



> bean标签的id能不能重复？
>
> * 不能！
>
> spring中写bean标签到底是怎么实例化对象的呢？
>
> * 默认情况下spring会通过反射机制，调用类的无参构造方法来实例化对象
> * 因为在写bean标签时会写class属性
>
> ```xml
> <!--写的bean标签-->
> <bean id="userDao" class="com.atguigu.dao.impl.userDaoImpl"/>
> ```
>
> ```java
> //实现原理如下：
> Class<?> clazz = Class.forName("com.atguigu.dao.impl.userDaoImpl");
> Object obj = clazz.newInstance();
> ```
>
>
> 在需要实例化的对象中需要有无参构造方法
>
> 在底层中会把创建好的对象存储到一个怎样的数据结构当中呢？
>
> * 会存储到一个map集合中
> * ![image-20241024184634692](C:\Users\heban\AppData\Roaming\Typora\typora-user-images\image-20241024184634692.png)
>
> 
>
> spring中配置文件的名字是可以随便取的，但也要符合命名规范xxx.xml
>
> 在配置文件中的配置类不是必须是自定义的，可以使用JDK中的类。
>
> 如果bead的id不存在，不会返回null，而是出现异常
>
>
> getBean()方法返回的类型是Object，如果访问子类中的特有方法或属性时，需要向下转型
>
> ```java
> //在指明id的时候同时指明类型。
> userDao userDao = context.getBeam("userDao",userDao.class);
> ```
>
> 
>
> 如果文件不在类路径当中，又该怎么配置文件呢？
>
> 系统盘中：
>
> ```java
> FileSystemXmlApplicationContext context = new FileSystemXmlApplicationContext("c:/spring.xml");
> ```
>
>
> spring底层的IoC是怎么实现的？
>
> * XML解析 + 工厂模式 + 反射机制
>
> 
>
> 默认情况下，不是在调用getBean()方法时才会实例化对象，在解析配置文件时就会实例化对象。
>
> 在`new ClassPathXmlApplicationContext("spring.xml");`时就会实例化配置文件中有的对象。



## spring6启用`Log4j2`日志框架

1. 引入`Log4j2`的依赖

   ```xml
   <!--log4j2的依赖-->
   <dependency>
     <groupId>org.apache.logging.log4j</groupId>
     <artifactId>log4j-core</artifactId>
     <version>2.19.0</version>
   </dependency>
   <dependency>
     <groupId>org.apache.logging.log4j</groupId>
     <artifactId>log4j-slf4j2-impl</artifactId>
     <version>2.19.0</version>
   </dependency>
   
   ```

2. 在类根路径下提供 log4j2.xml 配置文件，配置文件的文件名固定为：log4j2.xml，且文件必须放到类根路径下，配置文件的文件名是固定的，位置也是固定的，必须在类的根目录及其子目录下。
   ![image-20241024210903458](C:\Users\heban\AppData\Roaming\Typora\typora-user-images\image-20241024210903458.png)

   

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   
   <configuration>
       
       <loggers>
           <!--
               level指定日志级别，从低到高的优先级：
                   ALL < TRACE < DEBUG < INFO < WARN < ERROR < FATAL < OFF
               达到相应的级别才会输出日志信息
               级别越低输出的日志信息越多
           -->
   				<!-- 日志输出级别为 DEBUG，该级别之下的日志不会输出 -->
           <root level="DEBUG">
               <appender-ref ref="spring6log"/>
           </root>
       </loggers>
       
       <appenders>
           <!--输出日志信息到控制台-->
           <console name="spring6log" target="SYSTEM_OUT">
               <!--控制日志输出的格式-->
               <PatternLayout pattern="%d{yyyy-MM-dd HH:mm:ss SSS} [%t] %-3level %logger{1024} - %msg%n"/>
           </console>
       </appenders>
   
   </configuration>
   
   ```

   

自己怎么使用`Log4j2`记录日志呢？

1. 创建日志记录器对象

   ```java
   //注意是导入org.slf4j中的Logger类
   //获取Student类的日志记录器对象，也就是说只要是Student类中的代码执行记录日志的话，就会输出相关的日志信息
   Logger logger = LoggerFactory.getLogger(Student.class);
   ```

   

2. 记录日志，根据不同的级别来输出日志

   ```java
   public class LoggerTest {
   
       @Test
       public void test1(){
           Logger logger = LoggerFactory.getLogger(LoggerTest.class);
   
           logger.info("我是一条普通的信息");
           logger.debug("我是一条调试信息");
           logger.error("我是一条错误信息");
   
       }
   
   }
   /*
   当级别是DEBUG时输出的内容为
   Connected to the target VM, address: '127.0.0.1:52427', transport: 'socket'
   2024-10-24 21:29:08 787 [main] INFO com.atguigu.test.LoggerTest - 我是一条普通的信息
   2024-10-24 21:29:08 789 [main] DEBUG com.atguigu.test.LoggerTest - 我是一条调试信息
   2024-10-24 21:29:08 789 [main] ERROR com.atguigu.test.LoggerTest - 我是一条错误信息
   Disconnected from the target VM, address: '127.0.0.1:52427', transport: 'socket'
   
   三条信息都会输出
   
   当修改级别为ERROR后，输出的日志内容为
   Connected to the target VM, address: '127.0.0.1:52441', transport: 'socket'
   2024-10-24 21:30:48 114 [main] ERROR com.atguigu.test.LoggerTest - 我是一条错误信息
   Disconnected from the target VM, address: '127.0.0.1:52441', transport: 'socket'
   只输出了那条错误信息日志。
   */
   ```

   





## spring对IoC的实现

### 1.1依赖注入

1. set注入

   基于set方法实现的，底层会通过反射机制调用属性对应的set方法然后给属性赋值，这种注入方法要求属性必须对外提供set方法。

   > set方法的方法名除了前三个字母必须是set之外，后面的命名在符合命名规范的限制下是随便命名的。
   >
   >
   > 但是光写一个set方法是不行的，还需要在xml配置文件中配置信息调用set方法
   >
   > 如果在bean标签中需要用set注入，就需要写成双标签，
   >
   > 在双标签中写`<property name="set方法的方法名去掉set，然后把剩下的字母首字母小写，写到这里" ref="需要注入的bean的id"/>`标签
   > 

   

2. 构造方法注入

   通过类的构造方法，在实例化类的时候同时给属性赋值

   > 在bean双标签中写`<constructor-	arg ref="需要注入的bean的id">`标签，标签中的name属性是根据构造方法中参数的名字来进行注入的，标签中的index是根据构造方法中参数的索引来进行注入的（索引是从零开始），也可以什么也不写，直接让idea自己进行类的配对，但是这样会降低代码的可读性
   > ref属性是必须写的。



### set注入专题

#### 内部bean和外部bean

内部bean就是在<property>标签中嵌套一个<bean/>标签，外部bean就是直接使用ref引入的bean类。



#### 注入简单类型

注入简单类型就不能使用ref属性了，需要使用value属性，value="需要赋的值"。

但是在spring框架中哪些类型属于是简单类型呢？

![image-20241025120154888](C:\Users\heban\AppData\Roaming\Typora\typora-user-images\image-20241025120154888.png)

继承或者实现了这些的都属于是简单类型。八种基本类型（int...）、包装类型（Integer）、枚举类型、

Data可以作为简单类型，但是如果看作简单类型的话，使用value赋值，这个日期字符串的格式是有要求的，在实际开发中，一般不会把Data作为简单类型，虽然Data是简单类型，一般都是使用ref给Data类型的属性赋值。



#### 注入数组

```xml
<!--当数组属性中的元素类型是简单类型时，String-->
<property name="">
    <array>
    	<value>抽烟</value>
        <value>喝酒</value>
        <value>烫头</value>
    </array>
</property>
<!--当数组属性中的元素类型不是简单类型时-->
<property name="">
	<array>
        <!--bean中填写需要添加元素bean的id，w1、w2、w3分别在property的bean标签外部创建-->
    	<ref bean="w1"/>
        <ref bean="w2"/>
        <ref bean="w3"/>
    </array>
</property>
```



#### 注入List集合、Set集合、Map集合

和注入数组差不都，只是把<array>标签改为<list>或者<set>标签、<map>标签

在注入list集合时，如果在<list>标签中写了多个重复的值并不会报错

在注入Set集合时，在<set>标签中写了多个重复的值也不会报错，会自动去重。

在注入Map集合时，在<map>标签中加的和其他的不同，是加<entry>标签，<entry key="张三" value="12345678910"/>

在Map集合中，如果key和value不是简单类型就使用<entry key-ref="" value-ref=""/>在后面添加ref就行



#### 注入属性类对象

`Properties`

Properties本质上也是一个Map集合，Properties的父类是HashTable，HashTable实现了Map接口，虽然这也是一个Map集合，和Map集合的注入方式有点像，但是不同。 

```xml
<property>
    <!--Properties中的key和value只能是String类型-->
    <props>
        <prop key="">value</prop>
    </props 	>
    
</property>
```



#### 注入null和空字符串

不给属性注入数据默认注入为null

```xml
<!--这么做不是给name属性注入null，而是给name属性注入字符串，字符串内容为"null",如果想给属性注入null，直接不注入就行，不写下面这串代码就行-->
<property name="name" value="null"/>
```

手动注入null

```xml
<!--这样就是手动注入null-->
<property name="name">
    <null/>
</property>
```



注入空字符串

```xml
<!--注入空字符串第一种方式-->
<property name="name" value=""/>
<!--注入空字符串第二种方式-->
<property>
	<value/>
</property>
```



#### 注入特殊符号

第一种方式：

5个特殊字符对应的转义字符分别是：
![img](https://i-blog.csdnimg.cn/blog_migrate/debe090cb0843a96b53231ebc106a2c0.png)



第二种方式

```xml
<bean id="mathBean" class="com.powernode.spring6.bean.MathBean">
        <!--第一种方案：使用实体符号代替特殊符号-->
        <!--<property name="result" value="2 &lt; 3" />-->

        <!--第二种方案：使用<![CDATA[]]>,CDATA不是spring的语法，是xml中的规范-->
        <property name="result">
            <!--只能使用value标签-->
            <value><![CDATA[2 < 3]]></value>
        </property>
</bean>
```



### p命名空间注入

目的：简化配置，简化set注入的

p命名空间注入底层还是使用的set注入，只不过p命名空间注入可以让spring的配置变得更加简单



```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"<!--p命名空间注入要加入的就是这一行-->
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--
        第一步：在spring的配置文件头部添加p命名空间。 xmlns:p="http://www.springframework.org/schema/p"
        第二步：使用 p:属性名 = "属性值"，如果不是简单类型就在属性名后面加上-ref。
    -->
    <bean id="dogBean" class="com.powernode.spring6.bean.Dog" p:name="小花" p:age="3" p:birth-ref="birthBean"/>

    <!--这里获取的是当前系统时间。-->
    <bean id="birthBean" class="java.util.Date"/>

</beans>

```



### c命名空间注入

c命名空间注入是简化构造方法注入的

```xml
<!--
	第一步：在spring的配置文件头部添加c命名空间。xmlns:c="http://www.springframework.org/schema/c"
	第二步：使用c:属性名="属性值"，如果不是简单类型，与p命名空间一样在属性名后面加上-ref就行。
			c:_0 下标方式
			c:name 参数名方式
-->
```



### util命名空间注入

目的：让配置复用，主要针对集合

> 比如要写两个数据源
>
> ```java
> //第一个
> public class MyDataSource1 implements DataSource {
>     //一个属性类对象，是一个Map集合，键值都只能存储String类型
>     private Properties properties;
> 
>     public void setProperties(Properties properties) {
>         this.properties = properties;
>     }
>     //重写的方法在这里不展示
> }
> //第二个
> public class MyDataSource2 implements DataSource {
>     private Properties properties;
> 
>     public void setProperties(Properties properties) {
>         this.properties = properties;
>     }
> }
> ```
>
> 
>
> 在编写xml配置文件的时候,会出现这样的情况
>
> ```xml
> <?xml version="1.0" encoding="UTF-8"?>
> <beans xmlns="http://www.springframework.org/schema/beans"
>        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>        xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
> 
>         <bean id="ds1" class="com.atguigu.jdbc.MyDataSource1">
>             <property name="properties">
>                 <!--在两个bean标签中这一串是一样的，想在想能不能不重复写这种一样的信息-->
>                 <props>
>                     <prop key="driver">com.mysql.cj.jdbc.Driver</prop>
>                     <prop key="url">jdbc:mysql://localhost:3306/studb</prop>
>                     <prop key="username">root</prop>
>                     <prop key="password">abc123</prop>
>                 </props>
>             </property>
>         </bean>
> 
>         <bean id="ds2" class="com.atguigu.jdbc.MyDataSource2">
>             <property name="properties">
>                 <props>
>                     <prop key="driver">com.mysql.cj.jdbc.Driver</prop>
>                     <prop key="url">jdbc:mysql://localhost:3306/studb</prop>
>                     <prop key="username">root</prop>
>                     <prop key="password">abc123</prop>
>                 </props>
>             </property>
>         </bean>
> </beans>
> ```
>
> 
>
> util可以让配置复用
>
> ```xml
> <?xml version="1.0" encoding="UTF-8"?>
> <beans xmlns="http://www.springframework.org/schema/beans"
>        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>        xmlns:util="http://www.springframework.org/schema/util"
>        xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
>                             http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util.xsd">
> 
>         <!--引入util命名空间
>             在spring配置文件头部添加：
>             xmlns:util="http://www.springframework.org/schema/util"
>             http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util.xsd
>         -->
> 
>         <util:properties id="prop">
>             <prop key="driver">com.mysql.cj.jdbc.Driver</prop>
>             <prop key="url">jdbc:mysql://localhost:3306/studb</prop>
>             <prop key="username">root</prop>
>             <prop key="password">abc123</prop>
>         </util:properties>
> 
>         <bean id="ds1" class="com.atguigu.jdbc.MyDataSource1">
>             <property name="properties" ref="prop"/>
>         </bean>
> 
>         <bean id="ds2" class="com.atguigu.jdbc.MyDataSource2">
>             <property name="properties" ref="prop"/>
>         </bean>
> </beans>
> ```
>
> 



### 基于XML的自动装配

自动装配是基于set方法的



#### 根据名称进行自动装配

```xml
<!--根据名字进行自动装配-->
<!--注意：自动装配也是基于set方式实现的。如果要使用xml的自动装配就必须有set方法-->
<bean id="orderService" class="com.powernode.spring6.service.OrderService" autowire="byName"></bean>

<!--id一般也叫作bean的名称。-->
<!--根据名字进行自动装配的时候，被注入的对象的bean的id不能随便写，
		set方法的方法名去掉set，剩下单词首字母小写。-->
<bean id="orderDao" class="com.powernode.spring6.dao.OrderDao"/>

```



#### 基于类型进行自动装配

基于类型的自动装配时，在有效的配置文件中，某种类型的实例只能有一个对象，不然会报错

```xml
    <!--根据类型进行自动装配-->
    <!--自动装配是基于set方法的-->
    <!--根据类型进行自动装配的时候，在有效的配置文件当中，某种类型的实例只能有一个。-->
    <bean class="com.powernode.spring6.dao.VipDao"></bean>
    <bean id="x" class="com.powernode.spring6.dao.UserDao"></bean>
    <!--如果byType，根据类型装配时，如果配置文件中有两个类型一样的bean会报错-->
    <!--<bean id="y" class="com.powernode.spring6.dao.UserDao"></bean>-->
    <bean id="cs" class="com.powernode.spring6.service.CustomerService" autowire="byType"></bean>

```



### spring引入外部属性配置文件



```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd 
                            http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <!--引入外部的properties配置文件
        第一步：引入context命名空间，在配置文件的头部添加，
            xmlns:context="http://www.springframework.org/schema/context"
            http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd"
        第二步：使用标签context:property-placeholder的location属性来指定特定属性配置文件的路径
                location默认是从类的根目录下开始加载资源
    -->
    <context:property-placeholder location="jdbc.properties"/>

    <bean id="ds" class="com.atguigu.jdbc.MyDataSource">
        <property name="driver" value="${jdbc.driver}"/>
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>

</beans>
```

==但是在spring中使用${key}来加载配置文件中的数据时会默认先加载windows系统下的环境变量，所以在写配置文件时一般都会加前缀，不会直接写username这样的格式。==

```java
//properties配置文件没有前缀时
//输出结果为：MyDataSource{driver='com.mysql.cj.jdbc.Driver', url='jdbc:mysql://127.0.0.1:3306/atguigu', username='heban', password='abc123'}
//有前缀时的输出结果为：MyDataSource{driver='com.mysql.cj.jdbc.Driver', url='jdbc:mysql://127.0.0.1:3306/atguigu', username='root', password='abc123'}
```



## bean的作用域



#### spring的单例和多例

​	spring默认情况下Bean是单例（单例：`singleton`）的，在Spring上下文初始化的时候实例化（即在`new ClassPathXmlApplicationContext("spring.xml");`时），每一次调用getBean()方法时返回的都是那个单例对象。

如果不想采用默认的单例可以手动写为多例



**scope为singleton时，bean是在xml文件解析时就会实例化对象嘛？**

> 在Spring框架中，当一个bean的`scope`被设置为`singleton`时，这意味着Spring容器会为该bean创建一个且仅有一个的实例。然而，这并不意味着bean会在XML文件解析时立即被实例化。
>
> 以下是`singleton`作用域bean的创建和实例化过程：
>
> 1. **解析XML文件**：当Spring容器启动时，它会解析XML配置文件，读取所有的`<bean>`定义，但此时不会立即创建bean的实例。
> 2. **预实例化阶段**：对于设置了`lazy-init="false"`（这是默认值）的`singleton`作用域的bean，Spring容器在完成XML文件解析后，会进入预实例化阶段，这时会创建并初始化所有的非懒加载`singleton` beans。
> 3. **懒加载**：如果一个`singleton`作用域的bean设置了`lazy-init="true"`，则该bean不会在容器启动时被创建，而是在第一次被请求时才创建实例。
> 4. **第一次请求**：对于懒加载的bean，当应用程序首次通过容器请求该bean时，Spring容器会创建bean的实例，并进行依赖注入和初始化。
> 5. **后续请求**：一旦bean被创建，后续对该bean的请求都会返回同一个实例。
>
> 总结来说，`singleton`作用域的bean在XML文件解析时并不会立即实例化，除非它们被标记为非懒加载，且在容器启动后的预实例化阶段被创建。对于懒加载的`singleton` beans，它们会在第一次被请求时实例化。
>



​	将Bean的scope属性值设置为prototype：

1. bean变成多例
2. Spring上下文初始化的时候，并不会实例化这些prototype的Bean
3. 在每一次调用getBean()方法的时候，才会实例化该bean对象，而且每次调用getBean()获得的对象是不同的。



> prototype更多的细节：
>
> 1. **每次请求新实例**：与`singleton`作用域不同，`prototype`作用域的bean在每次请求（如通过`ApplicationContext.getBean()`）时都会创建一个新的实例。
> 2. **非单例**：`prototype`作用域意味着bean不是单例的，即容器中可以存在多个该bean的实例。
> 3. **依赖注入**：当你在一个`singleton`作用域的bean中通过`<ref>`标签引用一个`prototype`作用域的bean时，Spring容器会为这个引用创建一个新的`prototype` bean实例，并将其注入到`singleton` bean中。
> 4. **生命周期**：`prototype`作用域的bean的生命周期是由请求它们的对象管理的。Spring容器在创建`prototype` bean实例后，就不再管理这些实例的生命周期。
> 5. **销毁**：`prototype`作用域的bean不会自动调用销毁回调方法（如`@PreDestroy`注解的方法或配置的`destroy-method`），因为它们不是由Spring容器管理的。
>
> 因此，当你在XML配置中使用`<ref>`标签引用一个`prototype`作用域的bean时，Spring容器会确保每次引用都返回一个新的实例，而不是共享同一个实例。这允许你在应用程序的不同部分使用不同的`prototype` bean实例，每个实例都有自己的状态和生命周期。





> 目前scope属性有两个值
>
> 一个是singleton 单例/默认情况下就是单例的
>
> 另一个是prototype 原型/多例
>
> 还有其他的值，session和request，但是这两个值是在web项目中才有，比如使用springmvc框架就会有这两个值
> ![image-20241029103935905](C:\Users\heban\AppData\Roaming\Typora\typora-user-images\image-20241029103935905.png)



##### 了解的内容

* 单例的scope在不同线程中使用getBean()获取的都是同一个bean对象，如果想要在不同的线程中getBean()获取的是不同的bean对象则需要使用自定义的scope（想要线程安全的话）

  > 自定义一个scope的步骤
  >
  > 1. 自定义scope需要实现scope接口，spring内置了一个线程范围的类：org.springframework.context.support.SimpleThreanScope，可以直接使用
  >
  > 2. 将自定义的scope注册到IoC容器中
  >
  > 3. 使用scope
  >
  >    ```xml
  >    <?xml version="1.0" encoding="UTF-8"?>
  >    <beans xmlns="http://www.springframework.org/schema/beans"
  >           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  >           xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
  >                                                                                                                                                                            
  >        <!--配置我们自定义的作用域-->
  >        <!-- CustomScopeConfigurer用户自定义的范围配置器 -->
  >    		<!-- 将自定义作用域注入该配置器中，以便可以使用 -->
  >        <bean class="org.springframework.beans.factory.config.CustomScopeConfigurer">
  >            <property name="scopes">
  >                <map>
  >                    <!-- key为使用自定义范围时的名 -->
  >                    <entry key="threadScope">
  >                        <!--这个Scope接口的实现类使用的是Spring框架内置的。也可以自定义。-->
  >                        <bean class="org.springframework.context.support.SimpleThreadScope"/>
  >                    </entry>
  >                </map>
  >            </property>
  >        </bean>
  >                                                                                                                                                                                
  >        <!-- 第三步：使用Scope。 -->
  >        <bean id="sb" class="com.powernode.spring6.bean.SpringBean" scope="threadScope"></bean>
  >                                                                                                                                                                            
  >    </beans>
  >                                                                                                                                                                            
  >    ```
  >
  >    



### Spring中的单例bean是线程安全的吗？

对于一个bean可以用@Scope指定是单例还是多例

```java
@Service
@Scope("singleton")//多例的话指定为prototype
public class UserServiceImpl implement UserService{
    
}
```



如果在Spring的bean中定义了成员变量，没有使用static修饰，那就是线程不安全的。如果bean中只有方法，没有变量，那就是线程安全的。



## GoF之工厂模式

* 设计模式：一种可以被重复利用的解决方案
* GoF（Gang of Four），中文名--四人组，包含了23种设计模式
* 平常说的设计模式指的就是这23种设计模式
* 除了GoF设计模式外（23种设计模式），还有其他的设计模式，比如：JavaEE的设计模式（DAO模式、MVC模式等）



### 分类

GoF23种设计模式可以分为三大类（==面试可能会问的==）：

* **创建型**（5个）：解决对象创建问题
  * 单例模式
  * 工厂方法模式
  * 抽象工厂模式
  * 建造者模式
  * 原型模式
* **结构型**（7个）：一些类或对象组合在一起的经典结构。
  * 代理模式
  * 装饰模式
  * 适配器模式
  * 组合模式
  * 享元模式
  * 外观模式
  * 桥接模式
* **行为型**（11个）：解决类或对象之间的交互问题
  * 策略模式
  * 模板方法模式
  * 责任链模式
  * 观察者模式
  * 迭代子模式
  * 命令模式
  * 备忘录模式
  * 状态模式
  * 访问者模式
  * 中介者模式
  * 解释器模式



java中的IO库就使用了适配器模式和装饰模式。

工厂模式是解决创建对象问题的，所以工厂模式属于创建型设计模式，

在Spring框架底层使用了大量的工厂模式



### 工厂模式的三种形态

工厂模式通常有三种形态：

* 第一种：**简单工厂模式**（Simple Factory）：不属于23种设计模式之一，简单工厂模式又叫做：静态工厂方法模式。==**简单工厂模式是工厂方法模式的一种特殊实现**==
* 第二种：**工厂方法模式**（Factory Method）：是23种设计模式之一。
* 第三种：**抽象工厂模式**（Abstract Factory）：是23种设计模式之一。





### 简单工厂模式

简单工厂模式中的角色：

- 抽象产品角色
- 具体产品角色
- 工厂类角色



>  优点：客户端程序不需要关心对象的创建细节，需要哪个对象时，只需要向工厂索要即可，即初步实现了责任的分离。客户端只负责“消费”，工厂负责“生产”，生产和消费分离。
>
> 缺点：假设现在需要扩展一个新的产品，工厂类的代码是需要修改的，这违背了OCP原则。
>
> ​			工厂类的责任比较重大，不能出现任何问题，因为这个工厂类负责所有的产品的生产，称为全能类或上帝类，这个工厂类一旦出现问题，整个系统就会瘫痪。



简单工厂模式的代码如下：

抽象产品角色：

- Weapon

```java
package com.powernode.factory;

/**
 * 武器（抽象产品角色）
 * @author 动力节点
 * @version 1.0
 * @className Weapon
 * @since 1.0
 **/
public abstract class Weapon {
    /**
     * 所有的武器都有攻击行为
     */
    public abstract void attack();
}
```

具体产品角色：

- Tank

```java
package com.powernode.factory;

/**
 * 坦克（具体产品角色）
 * @author 动力节点
 * @version 1.0
 * @className Tank
 * @since 1.0
 **/
public class Tank extends Weapon{
    @Override
    public void attack() {
        System.out.println("坦克开炮！");
    }
}
```

- Fighter

```java
package com.powernode.factory;

/**
 * 战斗机（具体产品角色）
 * @author 动力节点
 * @version 1.0
 * @className Fighter
 * @since 1.0
 **/
public class Fighter extends Weapon{
    @Override
    public void attack() {
        System.out.println("战斗机投下原子弹！");
    }
}
```

- Dagger

```java
package com.powernode.factory;

/**
 * 匕首（具体产品角色）
 * @author 动力节点
 * @version 1.0
 * @className Dagger
 * @since 1.0
 **/
public class Dagger extends Weapon{
    @Override
    public void attack() {
        System.out.println("砍他丫的！");
    }
}
```

工厂类角色：

- WeaponFactory

```java
package com.powernode.factory;

/**
 * 工厂类角色
 * @author 动力节点
 * @version 1.0
 * @className WeaponFactory
 * @since 1.0
 **/
public class WeaponFactory {
    /**
     * 根据不同的武器类型生产武器
     * @param weaponType 武器类型
     * @return 武器对象
     */
    public static Weapon get(String weaponType){
        if (weaponType == null || weaponType.trim().length() == 0) {
            return null;
        }
        Weapon weapon = null;
        if ("TANK".equals(weaponType)) {
            weapon = new Tank();
        } else if ("FIGHTER".equals(weaponType)) {
            weapon = new Fighter();
        } else if ("DAGGER".equals(weaponType)) {
            weapon = new Dagger();
        } else {
            throw new RuntimeException("不支持该武器！");
        }
        return weapon;
    }
}
```

测试程序（客户端程序）：

- Client

```java
package com.powernode.factory;

/**
 * @author 动力节点
 * @version 1.0
 * @className Client
 * @since 1.0
 **/
public class Client {
    public static void main(String[] args) {
        Weapon weapon1 = WeaponFactory.get("TANK");
        weapon1.attack();
 
        Weapon weapon2 = WeaponFactory.get("FIGHTER");
        weapon2.attack();

        Weapon weapon3 = WeaponFactory.get("DAGGER");
        weapon3.attack();
    }
}
```

执行结果：

![image.png](https://gitee.com/lyxbiu/spring6/raw/master/Spring.assets/image-1704526785323.png)





### 工厂方法模式 



>  工厂方法模式可以解决简单工厂模式中违背OCP原则的问题
>
> 解决方法就是一个工厂只生产一种产品，这样工厂就不是全能类、上帝类了，同时符合OCP原则。



工厂方法模式中的角色：

- 抽象产品角色		eg  Weapon
- 具体产品角色        eg  Dagger Weapon
- 抽象工厂角色        eg  WeaponFactory
- 具体工厂角色        eg  DaggerFactory  TankFactory







优点：当扩展一个产品的时候，符合OCP原则，因为只需要添加两个类，一个类是具体产品类，一个类是具体工厂类，都是添加类，没有修改之前的代码，符合OCP原则。

缺点：每次增加一个产品时，都需要增加一个具体类和对象实现工厂，使得系统中类的个数成倍增加，在一定程度上增加了系统的复杂性，同时也增加了系统具体类的依赖，这不是什么好事。



### 抽象工厂模式（了解）

抽象工厂模式相对于工厂方法模式来说，就是工厂方法模式是针对一个产品系列的，而抽象工厂模式是针对多个产品系列的，即工厂方法模式是一个产品系列一个工厂类，而抽象工厂模式是多个产品系列一个工厂类。

抽象工厂模式特点：抽象工厂模式是所有形态的工厂模式中最为抽象和最具一般性的一种形态。抽象工厂模式是指当有多个抽象角色时，使用的一种工厂模式。抽象工厂模式可以向客户端提供一个接口，使客户端在不必指定产品的具体的情况下，创建多个产品族中的产品对象。它有多个抽象产品类，每个抽象产品类可以派生出多个具体产品类，一个抽象工厂类，可以派生出多个具体工厂类，每个具体工厂类可以创建多个具体产品类的实例。每一个模式都是针对一定问题的解决方案，工厂方法模式针对的是一个产品等级结构；而抽象工厂模式针对的是多个产品等级结果。

抽象工厂中包含4个角色：

- 抽象工厂角色
- 具体工厂角色
- 抽象产品角色
- 具体产品角色

抽象工厂模式的类图如下：

![image.png](https://gitee.com/lyxbiu/spring6/raw/master/Spring.assets/image-1704527115793.png)

抽象工厂模式代码如下：

第一部分：武器产品族

```java
package com.powernode.product;

/**
 * 武器产品族
 * @author 动力节点
 * @version 1.0
 * @className Weapon
 * @since 1.0
 **/
public abstract class Weapon {
    public abstract void attack();
}
package com.powernode.product;

/**
 * 武器产品族中的产品等级1
 * @author 动力节点
 * @version 1.0
 * @className Gun
 * @since 1.0
 **/
public class Gun extends Weapon{
    @Override
    public void attack() {
        System.out.println("开枪射击！");
    }
}
package com.powernode.product;

/**
 * 武器产品族中的产品等级2
 * @author 动力节点
 * @version 1.0
 * @className Dagger
 * @since 1.0
 **/
public class Dagger extends Weapon{
    @Override
    public void attack() {
        System.out.println("砍丫的！");
    }
}
```

第二部分：水果产品族

```java
package com.powernode.product;

/**
 * 水果产品族
 * @author 动力节点
 * @version 1.0
 * @className Fruit
 * @since 1.0
 **/
public abstract class Fruit {
    /**
     * 所有果实都有一个成熟周期。
     */
    public abstract void ripeCycle();
}
package com.powernode.product;

/**
 * 水果产品族中的产品等级1
 * @author 动力节点
 * @version 1.0
 * @className Orange
 * @since 1.0
 **/
public class Orange extends Fruit{
    @Override
    public void ripeCycle() {
        System.out.println("橘子的成熟周期是10个月");
    }
}
package com.powernode.product;

/**
 * 水果产品族中的产品等级2
 * @author 动力节点
 * @version 1.0
 * @className Apple
 * @since 1.0
 **/
public class Apple extends Fruit{
    @Override
    public void ripeCycle() {
        System.out.println("苹果的成熟周期是8个月");
    }
}
```

第三部分：抽象工厂类

```java
package com.powernode.factory;

import com.powernode.product.Fruit;
import com.powernode.product.Weapon;

/**
 * 抽象工厂
 * @author 动力节点
 * @version 1.0
 * @className AbstractFactory
 * @since 1.0
 **/
public abstract class AbstractFactory {
    public abstract Weapon getWeapon(String type);
    public abstract Fruit getFruit(String type);
}
```

第四部分：具体工厂类

```java
package com.powernode.factory;

import com.powernode.product.Dagger;
import com.powernode.product.Fruit;
import com.powernode.product.Gun;
import com.powernode.product.Weapon;

/**
 * 武器族工厂
 * @author 动力节点
 * @version 1.0
 * @className WeaponFactory
 * @since 1.0
 **/
public class WeaponFactory extends AbstractFactory{

    public Weapon getWeapon(String type){
        if (type == null || type.trim().length() == 0) {
            return null;
        }
        if ("Gun".equals(type)) {
            return new Gun();
        } else if ("Dagger".equals(type)) {
            return new Dagger();
        } else {
            throw new RuntimeException("无法生产该武器");
        }
    }

    @Override
    public Fruit getFruit(String type) {
        return null;
    }
}
package com.powernode.factory;

import com.powernode.product.*;

/**
 * 水果族工厂
 * @author 动力节点
 * @version 1.0
 * @className FruitFactory
 * @since 1.0
 **/
public class FruitFactory extends AbstractFactory{
    @Override
    public Weapon getWeapon(String type) {
        return null;
    }

    public Fruit getFruit(String type){
        if (type == null || type.trim().length() == 0) {
            return null;
        }
        if ("Orange".equals(type)) {
            return new Orange();
        } else if ("Apple".equals(type)) {
            return new Apple();
        } else {
            throw new RuntimeException("我家果园不产这种水果");
        }
    }
}
```

第五部分：客户端程序

```java
package com.powernode.client;

import com.powernode.factory.AbstractFactory;
import com.powernode.factory.FruitFactory;
import com.powernode.factory.WeaponFactory;
import com.powernode.product.Fruit;
import com.powernode.product.Weapon;

/**
 * @author 动力节点
 * @version 1.0
 * @className Client
 * @since 1.0
 **/
public class Client {
    public static void main(String[] args) {
        // 客户端调用方法时只面向AbstractFactory调用方法。
        AbstractFactory factory = new WeaponFactory(); // 注意：这里的new WeaponFactory()可以采用 简单工厂模式 进行隐藏。
        Weapon gun = factory.getWeapon("Gun");
        Weapon dagger = factory.getWeapon("Dagger");

        gun.attack();
        dagger.attack();

        AbstractFactory factory1 = new FruitFactory(); // 注意：这里的new FruitFactory()可以采用 简单工厂模式 进行隐藏。
        Fruit orange = factory1.getFruit("Orange");
        Fruit apple = factory1.getFruit("Apple");

        orange.ripeCycle();
        apple.ripeCycle();
    }
}
```

执行结果：

![image.png](https://gitee.com/lyxbiu/spring6/raw/master/Spring.assets/image-1704527258901.png)

抽象工厂模式的优缺点：

- 优点：当一个产品族中的多个对象被设计成一起工作时，它能保证客户端始终只使用同一个产品族中的对象。
- 缺点：产品族扩展非常困难，要增加一个系列的某一产品，既要在AbstractFactory里加代码，又要在具体的里面加代码。



## Spring的实例化（获取）方式

Spring为Bean提供了多种实例化方式，通常包括4种方式，也就是说在Spring中为Bean对象的创建准备了多种方案，为了更加灵活。

1. 通过构造方法实例化
2. 通过简单工厂模式实例化
3. 通过factory-bean实例化（工厂方法模式）
4. 通过FactoryBean接口实例化



#### 通过简单工厂模式实例化

Student类

```java
package com.atguigu.instantiation;

public class Student {

    public Student(){
        System.out.println("Student无参构造方法执行了！");
    }
}
```



StudentFactory

```java
package com.atguigu.instantiation;

public class StudentFactory {

    //写一个静态方法
    public static Student get(){
        //还是new了一个对象返回
        return new Student();
    }
}
```



xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="student" class="com.atguigu.instantiation.StudentFactory" factory-method="get"/>
    
</beans>
```



输出

```tex
Student无参构造方法执行了！
com.atguigu.instantiation.Student@6492fab5
```





#### 通过factory-bean实例化

通过factory-bean和factory-method属性共同完成

工厂方法模式中的抽象类先不写

具体类

Gun

```java
package com.atguigu.instantiation;

public class Gun {
    public Gun(){
        System.out.println("Gun的无参构造方法执行了！");
    }
}

```



GunFactory

```java
package com.atguigu.instantiation;

public class GunFactory {

    public Gun get(){
        return new Gun();
    }
}

```



xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

	<!--这是上面模式的bean对象，不是这个工厂方法模式的bean对象-->
    <bean id="student" class="com.atguigu.instantiation.StudentFactory" factory-method="get"/>

    <!--告诉Spring框架调用哪个对象的哪个方法来获取bean对象-->
    <bean id="gunFactory" class="com.atguigu.instantiation.GunFactory"/>
    <!--factory-bean属性告诉Spring调用哪个对象，factory-method告诉Spring调用该对象的哪个方法-->
    <bean id="gun" factory-bean="gunFactory" factory-method="get"/>

</beans>
<!--输出结果
	Gun的无参构造方法执行了！
	com.atguigu.instantiation.Gun@294e5088
-->
```





#### 通过FactoryBean接口实例化

当Spring容器遇到一个bean定义，其class属性指定为一个`FactoryBean`的实现时，它不会直接实例化这个bean，而是会调用这个`FactoryBean`实现的`getObject()`方法来获取bean的实例。

person类

```java
package com.atguigu.instantiation;

public class Person {
    public Person(){
        System.out.println("Person的无参构造方法执行了！");
    }
}
```



personFactoryBean类

```java
package com.atguigu.instantiation;

import org.springframework.beans.factory.FactoryBean;

public class PersonFactoryBean implements FactoryBean<Person> {
    @Override
    public Person getObject() throws Exception {
        return new Person();
    }

    @Override
    public Class<?> getObjectType() {
        return Person.class;
    }
}
```

xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="student" class="com.atguigu.instantiation.StudentFactory" factory-method="get"/>

    <!--告诉Spring框架调用哪个对象的哪个方法来获取bean对象-->
    <bean id="gunFactory" class="com.atguigu.instantiation.GunFactory"/>
    <!--factory-bean属性告诉Spring调用哪个对象，factory-method告诉Spring调用该对象的哪个方法-->
    <bean id="gun" factory-bean="gunFactory" factory-method="get"/>

    <!--第四种方式获取bean-->
    <!--实现了FactoryBean接口的类不需要再手动指定：factory-bean、factory-method属性-->
    <!--通过一个特殊的Bean：工厂Bean来返回一个普通Bean，Person对象-->
    <!--通过FactoryBean这个工厂类主要是想对普通的Bean进行加工处理-->
    <bean id="person" class="com.atguigu.instantiation.PersonFactoryBean"/>

</beans>
```





### BeanFactory和FactoryBean的区别

#### FactoryBean

FactoryBean是一个Bean，是一个能够**辅助Spring**实例化其他Bean对象的一个Bean。

在Spring中，Bean可以分为两种：

1. 普通Bean
2. 工厂Bean（工厂Bean也是一种Bean，只不过这种Bean比较特殊，它可以辅助Spring实例化其他Bean对象）

#### BeanFactory

Spring IoC容器的顶级接口，Bean工厂，在Spring IoC容器中Bean工厂负责创建Bean对象。





## Bean的生命周期



**可以在这个类`AbstractAutowireCapableBeanFactory`的`doCreateBean`()中查看bean的生命周期源码**

```java
protected Object doCreateBean(String beanName, RootBeanDefinition mbd, @Nullable Object[] args) throws BeanCreationException {
        BeanWrapper instanceWrapper = null;
        if (mbd.isSingleton()) {
            instanceWrapper = (BeanWrapper)this.factoryBeanInstanceCache.remove(beanName);
        }

        if (instanceWrapper == null) {
            instanceWrapper = this.createBeanInstance(beanName, mbd, args);
        }

        Object bean = instanceWrapper.getWrappedInstance();
        Class<?> beanType = instanceWrapper.getWrappedClass();
        if (beanType != NullBean.class) {
            mbd.resolvedTargetType = beanType;
        }

        synchronized(mbd.postProcessingLock) {
            if (!mbd.postProcessed) {
                try {
                    this.applyMergedBeanDefinitionPostProcessors(mbd, beanType, beanName);
                } catch (Throwable var17) {
                    Throwable ex = var17;
                    throw new BeanCreationException(mbd.getResourceDescription(), beanName, "Post-processing of merged bean definition failed", ex);
                }

                mbd.markAsPostProcessed();
            }
        }

        boolean earlySingletonExposure = mbd.isSingleton() && this.allowCircularReferences && this.isSingletonCurrentlyInCreation(beanName);
        if (earlySingletonExposure) {
            if (this.logger.isTraceEnabled()) {
                this.logger.trace("Eagerly caching bean '" + beanName + "' to allow for resolving potential circular references");
            }
			//把单例对象缓存起来
            this.addSingletonFactory(beanName, () -> {
                return this.getEarlyBeanReference(beanName, mbd, bean);
            });
        }

        Object exposedObject = bean;

        try {
            //给bean的属性赋值
            this.populateBean(beanName, mbd, instanceWrapper);
            exposedObject = this.initializeBean(beanName, exposedObject, mbd);
        } catch (Throwable var18) {
            Throwable ex = var18;
            if (ex instanceof BeanCreationException bce) {
                if (beanName.equals(bce.getBeanName())) {
                    throw bce;
                }
            }

            throw new BeanCreationException(mbd.getResourceDescription(), beanName, ex.getMessage(), ex);
        }

        if (earlySingletonExposure) {
            Object earlySingletonReference = this.getSingleton(beanName, false);
            if (earlySingletonReference != null) {
                if (exposedObject == bean) {
                    exposedObject = earlySingletonReference;
                } else if (!this.allowRawInjectionDespiteWrapping && this.hasDependentBean(beanName)) {
                    String[] dependentBeans = this.getDependentBeans(beanName);
                    Set<String> actualDependentBeans = new LinkedHashSet(dependentBeans.length);
                    String[] var12 = dependentBeans;
                    int var13 = dependentBeans.length;

                    for(int var14 = 0; var14 < var13; ++var14) {
                        String dependentBean = var12[var14];
                        if (!this.removeSingletonIfCreatedForTypeCheckOnly(dependentBean)) {
                            actualDependentBeans.add(dependentBean);
                        }
                    }

                    if (!actualDependentBeans.isEmpty()) {
                        throw new BeanCurrentlyInCreationException(beanName, "Bean with name '" + beanName + "' has been injected into other beans [" + StringUtils.collectionToCommaDelimitedString(actualDependentBeans) + "] in its raw version as part of a circular reference, but has eventually been wrapped. This means that said other beans do not use the final version of the bean. This is often the result of over-eager type matching - consider using 'getBeanNamesForType' with the 'allowEagerInit' flag turned off, for example.");
                    }
                }
            }
        }

        try {
            this.registerDisposableBeanIfNecessary(beanName, bean, mbd);
            return exposedObject;
        } catch (BeanDefinitionValidationException var16) {
            throw new BeanCreationException(mbd.getResourceDescription(), beanName, "Invalid destruction signature", var16);
        }
    }
```



bean不同的作用域会有不同的管理方式

Spring容器只对singleton（单例）的bean进行完整的生命周期管理

如果是Prototype（多例）作用域的bean，Spring容器只负责将该bean初始化完毕。等客户端程序一旦获取到该bean之后，Spring容器就不再管理该对象的生命周期了，最后两步（使用后）不管了。





### bean的生命周期之五步

实例化Bean--->给对象Bean的属性赋值--->初始化Bean---->使用Bean----->销毁Bean



实现类

```java
package com.atguigu.instantiation;

import org.springframework.beans.BeansException;
import org.springframework.beans.factory.*;

import java.util.Set;

public class User implements BeanNameAware, BeanFactoryAware, BeanClassLoaderAware , InitializingBean,DisposableBean {
    private String name;

    public User() {
        System.out.println("第一步：实例化User对象！");
    }

    public void setName(String name) {
        System.out.println("第二步：给对象的属性赋值！");
        this.name = name;
    }

    public void initBean(){
        System.out.println("第三步：初始化Bean！");
    }

    public void destroyBean(){
        System.out.println("第五步：销毁Bean！");
    }

    @Override
    public void setBeanClassLoader(ClassLoader classLoader) {
        System.out.println("bean对象的加载器：" + classLoader);
    }

    @Override
    public void setBeanFactory(BeanFactory beanFactory) throws BeansException {
        System.out.println("bean的bean工厂：" + beanFactory);
    }

    @Override
    public void setBeanName(String name) {
        System.out.println("bean的名字：" + name);
    }

    @Override
    public void destroy() throws Exception {
        System.out.println("执行了bean周期中的DisPosable接口的方法destroy()方法");
    }

    @Override
    public void afterPropertiesSet() throws Exception {
        System.out.println("执行了bean周期中的initializingBean接口的方法afterPropertiesSet()");
    }
}

```



xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--初始化和销毁方法需要自己写自己配，在bean标签中声明方法名-->
    <bean id="user" class="com.atguigu.instantiation.User" init-method="initBean" destroy-method="destroyBean">
        <property name="name" value="张三"/>
    </bean>
</beans>
```



测试类

```java
 @Test
public void test4(){
    ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("Spring-instantiation.xml");
    User user = context.getBean("user", User.class);
    System.out.println("第四步：使用对象Bean\n" + user);

    //如果需要销毁bean的话需要手动关闭IoC容器，
    // ApplicationContext里面没有close方法，所以使用会报错，需要转为ClassPathXmlApplicationContext
    context.close();
}

/*输出结果
第一步：实例化User对象！
第二步：给对象的属性赋值！
第三步：初始化Bean！
第四步：使用对象Bean
com.atguigu.instantiation.User@c2db68f
第五步：销毁Bean！
*/
```



### bean的生命周期之七步

1. 实例化Bean
2. 给Bean对象赋值
3. 执行“Bean后处理器”的before方法
4. 初始化Bean
5. 执行“Bean后处理器”的after方法
6. 使用Bean
7. 销毁Bean



编写一个类实现BeanPostProcessor接口，然后重写before和after方法

```java
package com.atguigu.instantiation;

import org.springframework.beans.BeansException;
import org.springframework.beans.factory.config.BeanPostProcessor;

/**
 * 日志Bean后处理器
 */
public class LogBeanPostProcessor implements BeanPostProcessor {

    //方法有两个参数
    //第一个参数：刚创建的Bean对象
    //第二个参数：bean的名字
    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("执行Bean后处理器的before方法");
        return BeanPostProcessor.super.postProcessBeforeInitialization(bean, beanName);
    }

    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("执行bean后处理器的after方法");
        return BeanPostProcessor.super.postProcessAfterInitialization(bean, beanName);
    }
}

```

xml文件

```xml
<!--配置bean后处理器-->
<!--注意：这个bean后处理器将作用于整个配置文件中的所有bean-->
<bean class="com.atguigu.instantiation.LogBeanPostProcessor"/>
```



测试类

```java
@Test
public void test5(){
    ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("Spring-instantiation.xml");
    User user = context.getBean("user", User.class);
    System.out.println("第四步：使用Bean对象！");

    context.close();
}
/*
第一步：实例化User对象！
第二步：给对象的属性赋值！
执行Bean后处理器的before方法
第三步：初始化Bean！
执行bean后处理器的after方法
第四步：使用Bean对象！
第五步：销毁Bean！
*/
```





### bean生命周期之十步

1. 实例化Bean
2. 给bean的属性赋值
3. 检查bean是否实现了Aware的相关接口，并设置相关依赖
4. 执行bean处理器的before方法
5. 检查bean是否实现了initializingBean接口，并调用接口方法
6. 初始化bean
7. 执行bean处理器的after方法
8. 使用bean
9. 检查bean是否实现了DisposableBean接口，并调用接口方法
10. 销毁bean



#### Aware相关接口

Aware相关的接口包括：BeanNameAware、BeanClassLoaderAware、BeanFactoryAware

- 当Bean实现了BeanNameAware，Spring会将Bean的名字传递给Bean。
- 当Bean实现了BeanClassLoaderAware，Spring会将加载该Bean的类加载器传递给Bean。
- 当Bean实现了BeanFactoryAware，Spring会将Bean工厂对象传递给Bean。

实现了这些和下面的接口，会自动调用相应的重写的方法，这些方法会传递一些数据，更方便使用



#### InitializingBean接口

需要重写afterPropertiesSet()方法



#### DisposableBean接口

重写destroy()方法，该方法不调用close方法也是不会被调用的





### 让自己new的对象纳入Spring IoC容器中

使用DefaultListableBeanFactory

```java
Student student = new Student();

DefaultListableBeanFactory factory = new DefaultListableBeanFactory();
factory.registerSingleton("想要给对象的bean id",对象名);

//这样new出来的student对象就纳入了Spring IoC容器中
```





## Bean的循环依赖



![image-20241204153034563](C:\Users\heban\AppData\Roaming\Typora\typora-user-images\image-20241204153034563.png)



singleton + setter模式下的循环依赖是没有问题的

这个模式下会先创建对象，再给对象的属性赋值

> 这个模式下Spring对Bean的管理主要分为清晰的两个阶段：
>
> 第一阶段：在Spring容器加载的时候，实例化Bean，只要其中一个Bean实例化之后，马上就会“曝光”（不会等该Bean的属性赋值），也就是已经存在这个Bean对象，别人可以使用，只是属性值全部没有被赋值。
>
> 第二阶段：Bean“曝光”之后，再进行属性的赋值（调用set方法）
>
> 核心的解决方案：实例化对象和对象的属性赋值分为两个阶段完成。
>
> 注意：==**只有在scope为singleton的情况下，Bean才会采取提前“曝光”的措施**==，prototype不会提前“曝光”，因为多例只有在getBean的时候才会实例化，在xml文件中的<bean>标签中引用该多例对象时，该对象并没有实例化出来，是找不到的。就算实例化了，也会不知道调用哪一个bean对象，prototype是每getBean一次实例化一个新的对象



prototype + setter模式下

在ref的时候，就会实例化新的bean对象。

只有两个都是prototype的时候才会出现问题。其中有一个是singleton就会停止循环，两个都是双例的话，就会一直创建新的bean对象，不会用到先前创建的bean对象。



singleton + 构造方法模式下

只拿wife举例，husband一样

![image-20241031171715007](C:\Users\heban\AppData\Roaming\Typora\typora-user-images\image-20241031171715007.png)

![image-20241031171621157](C:\Users\heban\AppData\Roaming\Typora\typora-user-images\image-20241031171621157.png)

这种是有问题的，采用构造方法时，bean要实例化完成就需要执行完构造方法，因为采用构造方法实例化bean的话就会在实例化的时侯调用构造方法，即要完成构造方法里的赋值操作，wife里的构造方法需要使用husband对象，就需要实例化一个husband对象，但是在实例化husband的时候，在husband构造方法中又需要使用wife对象，可是wife有没有实例化完成，所以两个bean在实例化时都在等着对方实例化完成，就实例化不了，不能成功，**构造方法产生的循环依赖问题是不能被解决的**





### 源码分析

**添加bean单例对象到缓存中的源码方法**

```java
protected void addSingletonFactory(String beanName, ObjectFactory<?> singletonFactory) {
    Assert.notNull(singletonFactory, "Singleton factory must not be null");
    synchronized(this.singletonObjects) {
        if (!this.singletonObjects.containsKey(beanName)) {
            this.singletonFactories.put(beanName, singletonFactory);//往缓存中添加的动作就可以理解为曝光
            this.earlySingletonObjects.remove(beanName);
            this.registeredSingletons.add(beanName);
        }
    }
}
/*
这个方法是这个DefaultSingletonBeanRegistry类中的

DefaultSingletonBeanRegistry类中有三个重要的缓存
private final Map<String, Object> singletonObjects                   一级缓存
private final Map<String, Object> earlySingletonObjects				二级缓存
private final Map<String, ObjectFactory<?>> singletonFactories		 三级缓存

这三个缓存都是Map集合，Map集合中的key装的都是bean的name，也就是bean的id

一级缓存中存储的是：完整的单例Bean对象，也就是说这个缓存中的Bean对象的属性已经赋值了，是一个完整的Bean对象
二级缓存中存储的是：早期的单例Bean对象，这个缓存中的单例Bean对象的属性没有赋值，只是一个早期的实例对象
三级缓存中存储的是：单例工厂对象，这里面存储了大量的“工厂对象”，每一个单例Bean对象都会对应一个单例工厂对象，这个集合存储的是，创建该单例对象时对应的那个单例工厂对象 
*/
```





## Spring IoC注解式开发



### 注解回顾

注解怎么定义？

``` java
//标注注解的注解叫做元注解。
//@Target注解用来修饰@Component可以出现的位置，Target里面是可以放数组的，如下图一，
//以下表示@Component注解可以出现在类上、属性上
//@Target(value = {ElementType.TYPE,ElementType.FIELD})
//使用某个注解时，如果注解的属性名是value的话，value是可以省略的
//@Target({ElementType.TYPE,ElementType.FIELD})
//使用某个注解的时候，如果注解的属性值是数组，并且数组中只有一个元素，大括号可以省略。
@Target(ElementType.TYPE)
//@Retention也是一个元注解，用来标注@Component注解最终保留在class文件中，并且可以被反射机制读取
//@Retention注解只有一个值，不是数组
/*
SOURCE 源代码java文件，生成的class文件中就没有该信息了
CLASS class文件中会保留注解，但是jvm加载运行时就没有了
RUNTIME 运行时，如果想使用反射获取注解信息，则需要使用RUNTIME，反射是在运行阶段进行反射的
 */
@Retention(RetentionPolicy.RUNTIME)
public @interface Component{
    //这就定义了一个注解
    //而且在创建类的时候，框框中会有一个annotation选项，这就是选择生成一个注解
    //定义注解的属性
    //String是属性类型
    //name是属性名
    String name();
    
    //String[] 是属性类型
    //names是属性名
    String[] names();
    
}
```





#### 扫描包中的注解

``` java
package com.powernode.test;

import com.powernode.annotation.Component;

import java.io.File;
import java.net.URL;
import java.util.Arrays;
import java.util.Enumeration;
import java.util.HashMap;
import java.util.Map;

/**
 * @author 动力节点
 * @version 1.0
 * @className Test
 * @since 1.0
 **/
public class Test {
    public static void main(String[] args) throws Exception {
        // 存放Bean的Map集合。key存储beanId。value存储Bean。
        Map<String,Object> beanMap = new HashMap<>();

        String packageName = "com.powernode.bean";
        String path = packageName.replaceAll("\\.", "/");
        URL url = ClassLoader.getSystemClassLoader().getResource(path);
        File file = new File(url.getPath());
        File[] files = file.listFiles();
        Arrays.stream(files).forEach(f -> {
            String className = packageName + "." + f.getName().split("\\.")[0];
            try {
                Class<?> clazz = Class.forName(className);
                if (clazz.isAnnotationPresent(Component.class)) {
                    Component component = clazz.getAnnotation(Component.class);
                    String beanId = component.value();
                    Object bean = clazz.newInstance();
                    beanMap.put(beanId, bean);
                }
            } catch (Exception e) {
                e.printStackTrace();
            }
        });

        System.out.println(beanMap);
    }
}
```







### 声明Bean的注解

负责声明Bean的注解，常见的包括四个：

- @Component
- @Controller
- @Service
- @Repository

源码如下：

- @Component注解：

``` java
package com.powernode.annotation;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target(value = {ElementType.TYPE})
@Retention(value = RetentionPolicy.RUNTIME)
public @interface Component {
    String value();
}
```

- @Controller注解

```java
package org.springframework.stereotype;

import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
import org.springframework.core.annotation.AliasFor;

@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Component
public @interface Controller {
    @AliasFor(
        annotation = Component.class
    )
    String value() default "";
}
```

- @Service

```java
package org.springframework.stereotype;

import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
import org.springframework.core.annotation.AliasFor;

@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Component
public @interface Service {
    @AliasFor(
        annotation = Component.class
    )
    String value() default "";
}
```

- @Repository

```java
package org.springframework.stereotype;

import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
import org.springframework.core.annotation.AliasFor;

@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Component
public @interface Repository {
    @AliasFor(
        annotation = Component.class
    )
    String value() default "";
}
```



这些源码中的@AliasFor是表示别名的注解，这四个注解中@Component注解是老大，其他三个都是它的别名。

但是既然都是别名为什么还要分四个出来呢？其实是为了增强可读性，不同地方使用不同的注解可以增强可读性。





### Spring注解的使用

如何使用以上的注解呢？

- 第一步：加入aop的依赖
- 第二步：在配置文件中添加context命名空间
- 第三步：在配置文件中指定扫描的包
- 第四步：在Bean类上使用注解

#### **第一步：加上aop依赖**

我们可以看到当加入spring-context依赖之后，会关联加入aop的依赖。所以这一步不用做

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21376908/1665545268001-e3fb24f3-6688-4f52-a8c7-7c3084fa10a2.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_12%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10%2Fformat%2Cwebp)



#### **第二步：在配置文件中添加context命名空间**

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

</beans>
```



#### **第三步：在配置文件中指定要扫描的包**

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
    <context:component-scan base-package="com.powernode.spring6.bean"/>
</beans>
```

**如果是多个包怎么办？有两种解决方案：**

- **第一种：在配置文件中指定多个包，用逗号隔开。**

  ``` xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                             http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
      <context:component-scan base-package="com.powernode.spring6.bean,com.powernode.spring6.dao"/>
  </beans>
  ```

- **第二种：指定多个包的共同父包。但是这么写的话就要牺牲掉一些效率**

  ``` xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                             http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
      <context:component-scan base-package="com.powernode.spring6"/>
  </beans>
  ```





#### **第四步：在Bean类上使用注解**

``` java
package com.powernode.spring6.bean;

import org.springframework.stereotype.Component;

@Component(value = "userBean")
public class User {
}

/*
@Component相当于下面的配置
<bean id="user" class="com.powernode.spring6.bean.User"> </bean> 
*/
```

在写注解时，如果value值没有写，bean会有默认名称嘛？会有，就是类名首字母小写就是这个bean类的默认名称





### 选择性实例化Bean

假设在某个包下有很多Bean，有的Bean上标注了Component，有的标注了Controller，有的标注了Service，有的标注了Repository，现在由于某种特殊业务的需要，只允许其中所有的Controller参与Bean管理，其他的都不实例化。这应该怎么办呢？



为了方便把几个类定义在一个类中

``` java
package com.powernode.spring6.bean3;

import org.springframework.stereotype.Component;
import org.springframework.stereotype.Controller;
import org.springframework.stereotype.Repository;
import org.springframework.stereotype.Service;

@Component
public class A {
    public A() {
        System.out.println("A的无参数构造方法执行");
    }
}

@Controller
class B {
    public B() {
        System.out.println("B的无参数构造方法执行");
    }
}

@Service
class C {
    public C() {
        System.out.println("C的无参数构造方法执行");
    }
}

@Repository
class D {
    public D() {
        System.out.println("D的无参数构造方法执行");
    }
}

@Controller
class E {
    public E() {
        System.out.println("E的无参数构造方法执行");
    }
}

@Controller
class F {
    public F() {
        System.out.println("F的无参数构造方法执行");
    }
}
```

我只想实例化bean3包下的Controller。配置文件这样写：

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <context:component-scan base-package="com.powernode.spring6.bean3" use-default-filters="false">
        <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>
    
</beans>
```

use-default-filters="true" 表示：使用spring默认的规则，只要有Component、Controller、Service、Repository中的任意一个注解标注，则进行实例化。

**use-default-filters="false"** 表示：不再spring默认实例化规则，即使有Component、Controller、Service、Repository这些注解标注，也不再实例化。



也可以将use-default-filters设置为true（不写就是true），并且采用exclude-filter方式排出哪些注解标注的Bean不参与实例化：

``` xml
<context:component-scan base-package="com.powernode.spring6.bean3">
    <!--这里表示包含注解@Repository、@Service、@Controller三个注解失效-->
  <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Repository"/>
  <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Service"/>
  <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
</context:component-scan>
```



### 负责注入的注解

@Component @Controller @Service @Repository 这四个注解是用来声明Bean的，声明后这些Bean将被实例化。接下来我们看一下，如何给Bean的属性赋值。给Bean属性赋值需要用到这些注解：

- @Value
- @Autowired
- @Qualifier
- @Resource



#### **@Value**

当属性的类型是简单类型时，可以使用@Value注解进行注入。**使用@Value注解进行注入的话，可以不提供属性的set方法。**

@Value注解也可以使用在方法上。（set方法、构造方法上等）



#### **@Autowired与@Qualifier**

@Autowired注解可以用来注入**非简单类型**。被翻译为：自动连线的，或者自动装配。

单独使用@Autowired注解，**默认根据类型装配**。【默认是byType】

@Autowired注解中不需要写参数，但是@Qualifier注解中需要写注入的Bean的名字。并且也是不需要写set方法的。



@Autowired源码：

``` java
package org.springframework.beans.factory.annotation;

import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target({ElementType.CONSTRUCTOR, ElementType.METHOD, ElementType.PARAMETER, ElementType.FIELD, ElementType.ANNOTATION_TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface Autowired {
	boolean required() default true;
}
```

源码中有两处需要注意：

- 第一处：该注解可以标注在哪里？

  - 构造方法上

  - 方法上

  - 形参上

  - 属性上

  - 注解上
  - 如果一个类中构造方法只有一个，并且构造方法中的参数和属性都可以对应上，@Autowired注解可以省略不写，但一般不建议省略不写，省略这点干什么呢？真的是。

- 第二处：该注解有一个required属性，默认值是true，表示在注入的时候要求被注入的Bean必须是存在的，如果不存在则报错。如果required属性设置为false，表示注入的Bean存在或者不存在都没关系，存在的话就注入，不存在的话，也不报错。





#### @**Resource**

@Resource注解也可以完成非简单类型注入。那它和@Autowired注解有什么区别？

- @Resource注解是JDK扩展包中的，也就是说属于JDK的一部分。所以该注解是标准注解，更加具有通用性。(JSR-250标准中制定的注解类型。JSR是Java规范提案。)
- @Autowired注解是Spring框架自己的。
- **@Resource注解默认根据名称装配byName，未指定name时，使用属性名作为name。通过name找不到的话会自动启动通过类型byType装配。**
- **@Autowired注解默认根据类型装配byType，如果想根据名称装配，需要配合@Qualifier注解一起用。**
- @Resource注解用在属性上、setter方法上。
- @Autowired注解用在属性上、setter方法上、构造方法上、构造方法参数上。

@Resource注解属于JDK扩展包，所以不在JDK当中，需要额外引入以下依赖：【**如果是JDK8的话不需要额外引入依赖。高于JDK11或低于JDK8需要引入以下依赖。**】



一定要注意：**如果你用Spring6，要知道Spring6不再支持JavaEE，它支持的是JakartaEE9。（Oracle把JavaEE贡献给Apache了，Apache把JavaEE的名字改成JakartaEE了，大家之前所接触的所有的  javax.\*  包名统一修改为  jakarta.\*包名了。）**

如果使用的是Spring6+版本就导入这个依赖：

``` xml
<dependency>
  <groupId>jakarta.annotation</groupId>
  <artifactId>jakarta.annotation-api</artifactId>
  <version>2.1.1</version>
</dependency>
```

但是如果使用的是Spring5-版本的话，就需要导入这个依赖：

``` xml
<dependency>
  <groupId>javax.annotation</groupId>
  <artifactId>javax.annotation-api</artifactId>
  <version>1.3.2</version>
</dependency>
```





#### **全注解式开发**

所谓的全注解开发就是不再使用spring配置文件了。写一个配置类来代替配置文件。

配置类代替配置文件：

``` java
package com.powernode.spring6.config;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.ComponentScans;
import org.springframework.context.annotation.Configuration;

@Configuration//注解，标识是一个配置文件的类
@ComponentScan({"com.powernode.spring6.dao", "com.powernode.spring6.service"})//注解，标识需要扫描注解的包
public class Spring6Configuration {
}
```

写了配置类之后就不能继续`new ClassPathXmlApplicationContext()`,而是`new AnnotationConfigApplicationContext(配置类的class);`

``` java
@Test
public void testNoXml(){
    ApplicationContext applicationContext = new AnnotationConfigApplicationContext(Spring6Configuration.class);
    UserService userService = applicationContext.getBean("userService", UserService.class);
    userService.save();
}
```





## GoF代理模式



### 对代理模式的理解

**生活场景1**：牛村的牛二看上了隔壁村小花，牛二不好意思直接找小花，于是牛二找来了媒婆王妈妈。这里面就有一个非常典型的代理模式。牛二不能和小花直接对接，只能找一个中间人。其中王妈妈是代理类，牛二是目标类。王妈妈代替牛二和小花先见个面。（现实生活中的婚介所）【在程序中，对象A和对象B无法直接交互时。】

**生活场景2**：你刚到北京，要租房子，可以自己找，也可以找链家帮你找。其中链家是代理类，你是目标类。你们两个都有共同的行为：找房子。不过链家除了满足你找房子，另外会收取一些费用的。(现实生活中的房产中介)【在程序中，功能需要增强时。】

**西游记场景**：八戒和高小姐的故事。八戒要强抢民女高翠兰。悟空得知此事之后怎么做的？悟空幻化成高小姐的模样。代替高小姐与八戒会面。其中八戒是客户端程序。悟空是代理类。高小姐是目标类。那天夜里，在八戒眼里，眼前的就是高小姐，对于八戒来说，他是不知道眼前的高小姐是悟空幻化的，在他内心里这就是高小姐。所以悟空代替高小姐和八戒亲了嘴儿。这是非常典型的代理模式实现的保护机制。**代理模式中有一个非常重要的特点：对于客户端程序来说，使用代理对象时就像在使用目标对象一样。****【在程序中，目标需要被保护时】**

**业务场景**：系统中有A、B、C三个模块，使用这些模块的前提是需要用户登录，也就是说在A模块中要编写判断登录的代码，B模块中也要编写，C模块中还要编写，这些判断登录的代码反复出现，显然代码没有得到复用，可以为A、B、C三个模块提供一个代理，在代理当中写一次登录判断即可。代理的逻辑是：请求来了之后，判断用户是否登录了，如果已经登录了，则执行对应的目标，如果没有登录则跳转到登录页面。【在程序中，目标不但受到保护，并且代码也得到了复用。】

代理模式是GoF23种设计模式之一。属于结构型设计模式。

代理模式的作用是：为其他对象提供一种代理以控制对这个对象的访问。在某些情况下，一个客户不想或者不能直接引用一个对象，此时可以通过一个称之为“代理”的第三者来实现间接引用。代理对象可以在客户端和目标对象之间起到中介的作用，并且可以通过代理对象去掉客户不应该看到的内容和服务或者添加客户需要的额外服务。 通过引入一个新的对象来实现对真实对象的操作或者将新的对象作为真实对象的一个替身，这种实现机制即为代理模式，通过引入代理对象来间接访问一个对象，这就是代理模式的模式动机。

代理模式中的角色：

- 代理类（代理主题）
- 目标类（真实主题）
- 代理类和目标类的公共接口（抽象主题）：客户端在使用代理类时就像在使用目标类，不被客户端所察觉，所以代理类和目标类要有共同的行为，也就是实现共同的接口。

代理模式的类图：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21376908/1665651817094-af9ecbad-24ae-4c11-9fa2-efe46653df25.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_15%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10%2Fformat%2Cwebp)

代理模式在代码实现上，包括两种形式：

- 静态代理
- 动态代理



### 静态代理



![image-20241205205331597](C:\Users\heban\AppData\Roaming\Typora\typora-user-images\image-20241205205331597.png)

##### 缺点

使用静态代理容易类爆炸，如果系统中有1000个接口，那么每个接口都要有对应的代理类，这样的话类会急剧增加，不好维护。

所以怎么解决类爆炸问题？那就是使用动态代理。



### 动态代理

动态代理还是代理模式，只不过是添加了字节码生成技术，可以在内存中为我们动态生成一个class字节码，这个字节码就是代理类。

在内存中动态的生成字节码代理类的技术叫做：动态代理

在程序运行阶段，在内存中动态生成代理类，被称为动态代理，目的是为了减少代理类的数量。解决代码复用的问题。

在内存当中动态生成类的技术常见的包括：

- JDK动态代理技术：只能代理接口。
- CGLIB动态代理技术：CGLIB(Code Generation Library)是一个开源项目。是一个强大的，高性能，高质量的Code生成类库，它可以在运行期扩展Java类与实现Java接口。它既可以代理接口，又可以代理类，**底层是通过继承的方式实现的**。性能比JDK动态代理要好。**（底层有一个小而快的字节码处理框架ASM。）**
- Javassist动态代理技术：Javassist是一个开源的分析、编辑和创建Java字节码的类库。是由东京工业大学的数学和计算机科学系的 Shigeru Chiba （千叶 滋）所创建的。它已加入了开放源代码JBoss 应用服务器项目，通过使用Javassist对字节码操作为JBoss实现动态"AOP"框架。





#### JDK动态代理

我们还是使用静态代理中的例子：一个接口和一个实现类。

OrderService接口：

``` java
package com.powernode.mall.service;

/**
 * 订单接口
 * @author 动力节点
 * @version 1.0
 * @className OrderService
 * @since 1.0
 **/
public interface OrderService {
    /**
     * 生成订单
     */
    void generate();

    /**
     * 查看订单详情
     */
    void detail();

    /**
     * 修改订单
     */
    void modify();
}
```

OrderService接口实现类：

``` java
package com.powernode.mall.service.impl;

import com.powernode.mall.service.OrderService;

/**
 * @author 动力节点
 * @version 1.0
 * @className OrderServiceImpl
 * @since 1.0
 **/
public class OrderServiceImpl implements OrderService {
    @Override
    public void generate() {
        try {
            Thread.sleep(1234);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("订单已生成");
    }

    @Override
    public void detail() {
        try {
            Thread.sleep(2541);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("订单信息如下：******");
    }

    @Override
    public void modify() {
        try {
            Thread.sleep(1010);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("订单已修改");
    }
}
```

我们在静态代理的时候，除了以上一个接口和一个实现类之外，是不是要写一个代理类UserServiceProxy呀！在动态代理中UserServiceProxy代理类是可以动态生成的。这个类不需要写。我们直接写客户端程序即可：

客户端程序：

``` java
package com.powernode.mall;

import com.powernode.mall.service.OrderService;
import com.powernode.mall.service.impl.OrderServiceImpl;

import java.lang.reflect.Proxy;

/**
 * @author 动力节点
 * @version 1.0
 * @className Client
 * @since 1.0
 **/
public class Client {
    public static void main(String[] args) {
        // 第一步：创建目标对象
        OrderService target = new OrderServiceImpl();
        // 第二步：创建代理对象
        OrderService orderServiceProxy = Proxy.newProxyInstance(target.getClass().getClassLoader(), target.getClass().getInterfaces(), 调用处理器对象);
        // 第三步：调用代理对象的代理方法
        orderServiceProxy.detail();
        orderServiceProxy.modify();
        orderServiceProxy.generate();
    }
}
```

以上第二步创建代理对象是需要大家理解的：

`OrderService orderServiceProxy = Proxy.newProxyInstance(target.getClass().getClassLoader(), target.getClass().getInterfaces(), 调用处理器对象);`

这行代码做了两件事：

- 第一件事：在内存中生成了代理类的字节码
- 第二件事：创建代理对象

Proxy类全名：`java.lang.reflect.Proxy`。这是JDK提供的一个类（所以称为JDK动态代理）。主要是通过这个类在内存中生成代理类的字节码。

其中`newProxyInstance()`方法有三个参数：

- 第一个参数：类加载器。在内存中生成了字节码，要想执行这个字节码，也是需要先把这个字节码加载到内存当中的。所以要指定使用哪个类加载器加载。
- 第二个参数：接口类型。代理类和目标类实现相同的接口，所以要通过这个参数告诉JDK动态代理生成的类要实现哪些接口。
- 第三个参数：调用处理器。这是一个JDK动态代理规定的接口，接口全名：`java.lang.reflect.InvocationHandler`。显然这是一个回调接口，也就是说调用这个接口中方法的程序已经写好了，就差这个接口的实现类了。在这个例子中调用处理器中需要编写的就是增强代码（编写什么东西要看具体的情况，因为JDK动态代理技术没有那么神，它是猜不到你想要实现什么功能的）

所以接下来我们要写一下java.lang.reflect.InvocationHandler接口的实现类，并且实现接口中的方法，代码如下：

``` java
//TimerInvocationHandler
package com.powernode.mall.service;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;

/**
 * @author 动力节点
 * @version 1.0
 * @className TimerInvocationHandler
 * @since 1.0
 **/
public class TimerInvocationHandler implements InvocationHandler {
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        return null;
    }
}
```

InvocationHandler接口中有一个方法invoke，这个invoke方法上有三个参数：

- 第一个参数：Object proxy。代理对象。设计这个参数只是为了后期的方便，如果想在invoke方法中使用代理对象的话，尽管通过这个参数来使用。
- 第二个参数：Method method。目标方法。
- 第三个参数：Object[] args。目标方法调用时要传的参数。

这个invoke()方法什么时候被调用呢？就是在代理对象调用代理方法的时候就会被调用。这个方法是JDK自己调用的，不是我们调用。

我们将来肯定是要调用“目标方法”的，但要调用目标方法的话，需要“目标对象”的存在，“目标对象”从哪儿来呢？我们可以给TimerInvocationHandler提供一个构造方法，可以通过这个构造方法传过来“目标对象”，代码如下：

``` java
//TimerInvocationHandler
package com.powernode.mall.service;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;

/**
 * @author 动力节点
 * @version 1.0
 * @className TimerInvocationHandler
 * @since 1.0
 **/
public class TimerInvocationHandler implements InvocationHandler {
    // 目标对象
    private Object target;

    // 通过构造方法来传目标对象
    public TimerInvocationHandler(Object target) {
        this.target = target;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        return null;
    }
}
```

有了目标对象我们就可以在invoke()方法中调用目标方法了。代码如下：

``` java
//TimerInvocationHandler
package com.powernode.mall.service;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;

/**
 * @author 动力节点
 * @version 1.0
 * @className TimerInvocationHandler
 * @since 1.0
 **/
public class TimerInvocationHandler implements InvocationHandler {
    // 目标对象
    private Object target;

    // 通过构造方法来传目标对象
    public TimerInvocationHandler(Object target) {
        this.target = target;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        // 目标执行之前增强。
        long begin = System.currentTimeMillis();
        // 调用目标对象的目标方法
        Object retValue = method.invoke(target, args);
        // 目标执行之后增强。
        long end = System.currentTimeMillis();
        System.out.println("耗时"+(end - begin)+"毫秒");
        // 一定要记得返回哦。
        return retValue;
    }
}
```

到此为止，调用处理器就完成了。接下来，应该继续完善Client程序：

``` java
//客户端程序
package com.powernode.mall;

import com.powernode.mall.service.OrderService;
import com.powernode.mall.service.TimerInvocationHandler;
import com.powernode.mall.service.impl.OrderServiceImpl;

import java.lang.reflect.Proxy;

/**
 * @author 动力节点
 * @version 1.0
 * @className Client
 * @since 1.0
 **/
public class Client {
    public static void main(String[] args) {
        // 创建目标对象
        OrderService target = new OrderServiceImpl();
        // 创建代理对象
        OrderService orderServiceProxy = (OrderService) Proxy.newProxyInstance(target.getClass().getClassLoader(),
                                                                                target.getClass().getInterfaces(),
                                                                                new TimerInvocationHandler(target));
        // 调用代理对象的代理方法
        orderServiceProxy.detail();
        orderServiceProxy.modify();
        orderServiceProxy.generate();
    }
}
```

大家可能会比较好奇：那个InvocationHandler接口中的invoke()方法没看见在哪里调用呀？

注意：当你调用代理对象的代理方法的时候，注册在InvocationHandler接口中的invoke()方法会被调用。也就是上面代码第24 25 26行，这三行代码中任意一行代码执行，注册在InvocationHandler接口中的invoke()方法都会被调用。

执行结果：

![img](https://cdn.nlark.com/yuque/0/2022/png/21376908/1665715879232-21eb379f-c3a4-4ffc-868f-441079541feb.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_10%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)

学到这里可能会感觉有点懵，折腾半天，到最后这不是还得写一个接口的实现类吗？没省劲儿呀？

你要这样想就错了!!!!

我们可以看到，不管你有多少个Service接口，多少个业务类，这个TimerInvocationHandler接口是不是只需要写一次就行了，代码是不是得到复用了！！！！

而且最重要的是，以后程序员只需要关注核心业务的编写了，像这种统计时间的代码根本不需要关注。因为这种统计时间的代码只需要在调用处理器中编写一次即可。

到这里，JDK动态代理的原理就结束了。

不过我们看以下这个代码确实有点繁琐，对于客户端来说，用起来不方便：

![img](https://cdn.nlark.com/yuque/0/2022/png/21376908/1665716434406-4e092df4-b1a7-4d16-bbc1-1f134b8f51f7.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_37%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)

我们可以提供一个工具类：ProxyUtil，封装一个方法：

``` java
package com.powernode.mall.util;

import com.powernode.mall.service.TimerInvocationHandler;

import java.lang.reflect.Proxy;

/**
 * @author 动力节点
 * @version 1.0
 * @className ProxyUtil
 * @since 1.0
 **/
public class ProxyUtil {
    public static Object newProxyInstance(Object target) {
        return Proxy.newProxyInstance(target.getClass().getClassLoader(), 
                target.getClass().getInterfaces(), 
                new TimerInvocationHandler(target));
    }
}
```

这样客户端代码就不需要写那么繁琐了：

``` java
package com.powernode.mall;

import com.powernode.mall.service.OrderService;
import com.powernode.mall.service.TimerInvocationHandler;
import com.powernode.mall.service.impl.OrderServiceImpl;
import com.powernode.mall.util.ProxyUtil;

import java.lang.reflect.Proxy;

/**
 * @author 动力节点
 * @version 1.0
 * @className Client
 * @since 1.0
 **/
public class Client {
    public static void main(String[] args) {
        // 创建目标对象
        OrderService target = new OrderServiceImpl();
        // 创建代理对象
        OrderService orderServiceProxy = (OrderService) ProxyUtil.newProxyInstance(target);
        // 调用代理对象的代理方法
        orderServiceProxy.detail();
        orderServiceProxy.modify();
        orderServiceProxy.generate();
    }
}
```

执行结果：

![img](https://cdn.nlark.com/yuque/0/2022/png/21376908/1665716690080-a1fac908-d6d8-4605-b24d-2fd9fd19a7e6.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_13%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)







#### CGLIB动态代理

CGLIB既可以代理接口，又可以代理类。底层采用继承的方式实现。所以被代理的目标类不能使用final修饰。

使用CGLIB，需要引入它的依赖：

``` xml
<dependency>
  <groupId>cglib</groupId>
  <artifactId>cglib</artifactId>
  <version>3.3.0</version>
</dependency>
```

我们准备一个没有实现接口的类，如下：

``` java
package com.powernode.mall.service;

/**
 * @author 动力节点
 * @version 1.0
 * @className UserService
 * @since 1.0
 **/
public class UserService {

    public void login(){
        System.out.println("用户正在登录系统....");
    }

    public void logout(){
        System.out.println("用户正在退出系统....");
    }
}
```

使用CGLIB在内存中为UserService类生成代理类，并创建对象：

``` java
package com.powernode.mall;

import com.powernode.mall.service.UserService;
import net.sf.cglib.proxy.Enhancer;

/**
 * @author 动力节点
 * @version 1.0
 * @className Client
 * @since 1.0
 **/
public class Client {
    public static void main(String[] args) {
        // 创建字节码增强器
        Enhancer enhancer = new Enhancer();
        // 告诉cglib要继承哪个类
        enhancer.setSuperclass(UserService.class);
        // 设置回调接口
        enhancer.setCallback(方法拦截器对象);
        // 生成源码，编译class，加载到JVM，并创建代理对象
        UserService userServiceProxy = (UserService)enhancer.create();

        userServiceProxy.login();
        userServiceProxy.logout();

    }
}
```

和JDK动态代理原理差不多，在CGLIB中需要提供的不是InvocationHandler，而是：net.sf.cglib.proxy.MethodInterceptor

编写MethodInterceptor接口实现类：

``` java
package com.powernode.mall.service;

import net.sf.cglib.proxy.MethodInterceptor;
import net.sf.cglib.proxy.MethodProxy;

import java.lang.reflect.Method;

/**
 * @author 动力节点
 * @version 1.0
 * @className TimerMethodInterceptor
 * @since 1.0
 **/
public class TimerMethodInterceptor implements MethodInterceptor {
    @Override
    public Object intercept(Object target, Method method, Object[] objects, MethodProxy methodProxy) throws Throwable {
        return null;
    }
}
```

MethodInterceptor接口中有一个方法intercept()，该方法有4个参数：

第一个参数：目标对象

第二个参数：目标方法

第三个参数：目标方法调用时的实参

第四个参数：代理方法

在MethodInterceptor的intercept()方法中调用目标以及添加增强：

``` java
package com.powernode.mall.service;

import net.sf.cglib.proxy.MethodInterceptor;
import net.sf.cglib.proxy.MethodProxy;

import java.lang.reflect.Method;

/**
 * @author 动力节点
 * @version 1.0
 * @className TimerMethodInterceptor
 * @since 1.0
 **/
public class TimerMethodInterceptor implements MethodInterceptor {
    @Override
    public Object intercept(Object target, Method method, Object[] objects, MethodProxy methodProxy) throws Throwable {
        // 前增强
        long begin = System.currentTimeMillis();
        // 调用目标
        Object retValue = methodProxy.invokeSuper(target, objects);
        // 后增强
        long end = System.currentTimeMillis();
        System.out.println("耗时" + (end - begin) + "毫秒");
        // 一定要返回
        return retValue;
    }
}
```

回调已经写完了，可以修改客户端程序了：

``` java
package com.powernode.mall;

import com.powernode.mall.service.TimerMethodInterceptor;
import com.powernode.mall.service.UserService;
import net.sf.cglib.proxy.Enhancer;

/**
 * @author 动力节点
 * @version 1.0
 * @className Client
 * @since 1.0
 **/
public class Client {
    public static void main(String[] args) {
        // 创建字节码增强器
        Enhancer enhancer = new Enhancer();
        // 告诉cglib要继承哪个类
        enhancer.setSuperclass(UserService.class);
        // 设置回调接口
        enhancer.setCallback(new TimerMethodInterceptor());
        // 生成源码，编译class，加载到JVM，并创建代理对象
        UserService userServiceProxy = (UserService)enhancer.create();

        userServiceProxy.login();
        userServiceProxy.logout();

    }
}
```

对于高版本的JDK，如果使用CGLIB，需要在启动项中添加两个启动参数：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21376908/1665719287350-761d69a9-2666-40b3-9332-91d695f1eb86.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_20%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10%2Fformat%2Cwebp)

- --add-opens java.base/java.lang=ALL-UNNAMED
- --add-opens java.base/sun.net.util=ALL-UNNAMED

执行结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21376908/1665719690752-0b38d1ec-f4fd-4a8e-878c-3496da353fe2.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_15%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10%2Fformat%2Cwebp)









## 面向切面编程AOP

IoC使软件组件松耦合。AOP让你能够捕捉系统中经常使用的功能，把它转化成组件。

AOP（Aspect Oriented Programming）：面向切面编程，面向方面编程。（AOP是一种编程技术）

AOP是对OOP的补充延伸。

AOP底层使用的就是动态代理来实现的。

Spring的AOP使用的动态代理是：JDK动态代理 + CGLIB动态代理技术。Spring在这两种动态代理中灵活切换，如果是代理接口，会默认使用JDK动态代理，如果要代理某个类，这个类没有实现接口，就会切换使用CGLIB。当然，你也可以强制通过一些配置让Spring只使用CGLIB



### AOP介绍

一般一个系统当中都会有一些系统服务，例如：日志、事务管理、安全等。这些系统服务被称为：**交叉业务**

这些**交叉业务**几乎是通用的，不管你是做银行账户转账，还是删除用户数据。日志、事务管理、安全，这些都是需要做的。

如果在每一个业务处理过程当中，都掺杂这些交叉业务代码进去的话，存在两方面问题：

- 第一：交叉业务代码在多个业务流程中反复出现，显然这个交叉业务代码没有得到复用。并且修改这些交叉业务代码的话，需要修改多处。
- 第二：程序员无法专注核心业务代码的编写，在编写核心业务代码的同时还需要处理这些交叉业务。

使用AOP可以很轻松的解决以上问题。

请看下图，可以帮助你快速理解AOP的思想：

![img](https://cdn.nlark.com/yuque/0/2022/png/21376908/1665732609757-d8ae52ba-915e-49cf-9ef4-c7bcada0d601.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_25%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)

**用一句话总结AOP：将与核心业务无关的代码独立的抽取出来，形成一个独立的组件，然后以横向交叉的方式应用到业务流程当中的过程被称为AOP。**

**AOP的优点：**

- **第一：代码复用性增强。**
- **第二：代码易维护。**
- **第三：使开发者更关注业务逻辑。**



### AOP的七大术语

- **连接点 Joinpoint**
  - 在程序的整个执行流程中，**可以织入**切面的位置。方法的执行前后，异常抛出之后等位置。连接点描述的是位置
- **切点 Pointcut**
  - 在程序执行流程中，**真正织入**切面的方法。（一个切点对应多个连接点），切点本质上就是方法
- **通知 Advice**
  - 通知又叫增强，就是具体你要织入的代码（具体增强的代码），比如事务代码、日志代码、安全代码等。通知描述的是代码
  - 通知包括：

    - 前置通知（放在执行目标方法前面的代码）

    - 后置通知（放在执行目标方法后面的代码）

    - 环绕通知(环绕通知是最大的通知/范围最大，在前置通知之前，在后置通知之后)

    - 异常通知（在异常里面的代码，catch里面的代码，不是try里面的代码）

    - 最终通知(放在异常最后执行代码那里，就是finally语句块里面，不是catch，也不是try里面)
- **切面 Aspect**
  - **切点 + 通知就是切面。**
- 织入 Weaving
  - 把通知应用到目标对象上的过程。
- 代理对象 Proxy
  - 一个目标对象被织入通知后产生的新对象。
- 目标对象 Target
  - 被织入通知的对象。

通过下图，大家可以很好的理解AOP的相关术语

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21376908/1665735638342-44194599-66e2-4c02-a843-8a8b3ba5b0c8.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_17%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10%2Fformat%2Cwebp)





### 切点表达式

切点表达式用来定义通知（Advice）往哪些方法上切入。

切入点表达式语法格式：

``` tex
execution([访问控制权限修饰符] 返回值类型 [全限定类名]方法名(形式参数列表) [异常])
```

访问控制权限修饰符：

- 可选项。
- 没写，就是4个权限都包括。
- 写public就表示只包括公开的方法。

返回值类型：

- 必填项。
- \* 表示返回值类型任意。

全限定类名：

- 可选项。
- 两个点“..”代表当前包以及子包下的所有类。
- 省略时表示所有的类。

方法名：

- 必填项。
- *表示所有方法。
- set*表示所有的set方法。

形式参数列表：

- 必填项

- () 表示没有参数的方法
- (..) 参数类型和个数随意的方法
- (*) 只有一个参数的方法
- (*, String) 第一个参数类型随意，第二个参数是String的。

异常：

- 可选项。
- 省略时表示任意异常类型。

理解以下的切点表达式：

``` java
//service包下所有的类中以delete开始的所有方法
execution(public * com.powernode.mall.service.*.delete*(..))
```

``` java
//mall包下所有的类的所有的方法
execution(* com.powernode.mall..*(..))
```

``` java
//所有类的所有方法
execution(* *(..))
```







### 使用Spring中的AOP

Spring对AOP的实现包括以下3种方式：

- **第一种方式：Spring框架结合AspectJ框架实现的AOP，基于注解方式。**
- **第二种方式：Spring框架结合AspectJ框架实现的AOP，基于XML方式。**
- 第三种方式：Spring框架自己实现的AOP，基于XML配置方式。

实际开发中，都是Spring+AspectJ来实现AOP。所以我们重点学习第一种和第二种方式。

什么是AspectJ？（Eclipse组织的一个支持AOP的框架。AspectJ框架是独立于Spring框架之外的一个框架，Spring框架用了AspectJ） 

AspectJ项目起源于帕洛阿尔托（Palo Alto）研究中心（缩写为PARC）。该中心由Xerox集团资助，Gregor Kiczales领导，从1997年开始致力于AspectJ的开发，1998年第一次发布给外部用户，2001年发布1.0 release。为了推动AspectJ技术和社团的发展，PARC在2003年3月正式将AspectJ项目移交给了Eclipse组织，因为AspectJ的发展和受关注程度大大超出了PARC的预期，他们已经无力继续维持它的发展。



#### 准备工作

使用Spring+AspectJ的AOP需要引入的依赖如下：

``` xml
<!--pom.xml文件中-->
<!--spring context依赖-->
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-context</artifactId>
  <version>6.0.0-M2</version>
</dependency>
<!--spring aop依赖，这个依赖其实可以不用导入，导入上面的context依赖是会关联引入这个依赖-->
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-aop</artifactId>
  <version>6.0.0-M2</version>
</dependency>
<!--spring aspects依赖-->
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-aspects</artifactId>
  <version>6.0.0-M2</version>
</dependency>
```

Spring配置文件中添加context命名空间和aop命名空间

``` xml
<!--spring-aspectj-aop-annotation.xml-->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                           http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">

</beans>
```



#### 基于AspectJ的AOP注解式开发

##### 使用的注解

`@Aspect`，切面类是需要使用`@Aspect`注解进行标识的

`@before(切点表达式)`，使用这个注解标识的方法是一个前置通知



##### 实现步骤

第一步：定义目标类以及目标方法

``` java
//目标类
package com.powernode.spring6.service;

// 目标类
public class OrderService {
    // 目标方法
    public void generate(){
        System.out.println("订单已生成！");
    }
}
```

第二步：定义切面类

``` java
//切面类
package com.powernode.spring6.service;

import org.aspectj.lang.annotation.Aspect;

// 切面类
@Component
@Aspect
public class MyAspect {
}
```

第三步：目标类和切面类都纳入spring bean管理

​	在目标类OrderService上添加**@Component**注解。

​	在切面类MyAspect类上添加**@Component**注解。

第四步：在spring配置文件中添加组建扫描

``` xml 
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                           http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">
    <!--开启组件扫描-->
    <context:component-scan base-package="com.powernode.spring6.service"/>
</beans>
```

第五步：在切面类中添加通知

```  java
package com.powernode.spring6.service;

import org.springframework.stereotype.Component;
import org.aspectj.lang.annotation.Aspect;

// 切面类
@Aspect
@Component
public class MyAspect {
    // 这就是需要增强的代码（通知）
    public void advice(){
        System.out.println("我是一个通知");
    }
}
```

第六步：在通知上添加切点表达式

``` java
package com.powernode.spring6.service;

import org.aspectj.lang.annotation.Before;
import org.springframework.stereotype.Component;
import org.aspectj.lang.annotation.Aspect;

// 切面类
@Aspect
@Component
public class MyAspect {
    
    // 切点表达式
    @Before("execution(* com.powernode.spring6.service.OrderService.*(..))")
    // 这就是需要增强的代码（通知）
    public void advice(){
        System.out.println("我是一个通知");
    }
}
```

**注解@Before表示前置通知。**

第七步：在spring配置文件中启用自动代理

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                           http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd">
    <!--开启组件扫描-->
    <context:component-scan base-package="com.powernode.spring6.service"/>
    <!--开启自动代理-->
    <aop:aspectj-autoproxy proxy-target-class="true"/>
</beans>
```

**`<aop:aspectj-autoproxy  proxy-target-class="true"/>` 开启自动代理之后，Spring容器在扫描类的时候，凡事带有@Aspect注解的bean都会生成代理对象。**

**proxy-target-class="true" 表示强制采用cglib动态代理。**

**proxy-target-class="false" 表示采用jdk动态代理。默认值是false。即使写成false，当没有接口的时候，也会自动选择cglib生成代理类。**

测试程序：

``` java
package com.powernode.spring6.test;

import com.powernode.spring6.service.OrderService;
import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class AOPTest {
    @Test
    public void testAOP(){
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("spring-aspectj-aop-annotation.xml");
        OrderService orderService = applicationContext.getBean("orderService", OrderService.class);
        orderService.generate();
    }
}
```

运行结果：

![img](https://cdn.nlark.com/yuque/0/2022/png/21376908/1665843923087-e1116f09-2470-46cb-b21a-1526f62cab50.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_15%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)



##### 通知类型

通知类型包括：

- 前置通知：@Before 目标方法执行之前的通知
- 后置通知：@AfterReturning 目标方法执行之后的通知
- 环绕通知：@Around 目标方法之前添加通知，同时目标方法执行之后添加通知。
- 异常通知：@AfterThrowing 发生异常之后执行的通知
- 最终通知：@After 放在finally语句块中的通知

接下来，编写程序来测试这几个通知的执行顺序：

``` java
package com.powernode.spring6.service;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.*;
import org.springframework.stereotype.Component;

// 切面类
@Component
@Aspect
public class MyAspect {

    @Around("execution(* com.powernode.spring6.service.OrderService.*(..))")
    public void aroundAdvice(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
        System.out.println("环绕通知开始");
        // 执行目标方法。
        proceedingJoinPoint.proceed();
        System.out.println("环绕通知结束");
    }

    @Before("execution(* com.powernode.spring6.service.OrderService.*(..))")
    public void beforeAdvice(){
        System.out.println("前置通知");
    }

    @AfterReturning("execution(* com.powernode.spring6.service.OrderService.*(..))")
    public void afterReturningAdvice(){
        System.out.println("后置通知");
    }

    @AfterThrowing("execution(* com.powernode.spring6.service.OrderService.*(..))")
    public void afterThrowingAdvice(){
        System.out.println("异常通知");
    }

    @After("execution(* com.powernode.spring6.service.OrderService.*(..))")
    public void afterAdvice(){
        System.out.println("最终通知");
    }

}
```

``` java
//目标类和目标方法
package com.powernode.spring6.service;

import org.springframework.stereotype.Component;

// 目标类
@Component
public class OrderService {
    // 目标方法
    public void generate(){
        System.out.println("订单已生成！");
    }
}
```

``` java
//测试程序
package com.powernode.spring6.test;

import com.powernode.spring6.service.OrderService;
import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class AOPTest {
    @Test
    public void testAOP(){
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("spring-aspectj-aop-annotation.xml");
        OrderService orderService = applicationContext.getBean("orderService", OrderService.class);
        orderService.generate();
    }
}
```

执行结果：

![img](https://cdn.nlark.com/yuque/0/2022/png/21376908/1665892617792-22cc74a2-6876-4cd1-bb17-87d3b5211cae.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_19%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)

通过上面的执行结果就可以判断他们的执行顺序了，这里不再赘述。

结果中没有异常通知，这是因为目标程序执行过程中没有发生异常。我们尝试让目标方法发生异常：

``` java
package com.powernode.spring6.service;

import org.springframework.stereotype.Component;

// 目标类
@Component
public class OrderService {
    // 目标方法
    public void generate(){
        System.out.println("订单已生成！");
        if (1 == 1) {
            throw new RuntimeException("模拟异常发生");
        }
    }
}
```

再次执行测试程序，结果如下：

![img](https://cdn.nlark.com/yuque/0/2022/png/21376908/1665892847715-75045cd0-63b1-47f9-a77e-05911dc72339.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_24%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)

通过测试得知，当发生异常之后，最终通知也会执行，因为最终通知@After会出现在finally语句块中。

出现异常之后，**后置通知**和**环绕通知的结束部分**不会执行。



最后，其实其他的方法中也可以接收参数`JoinPoint joinPoint`,这和JoinPoint在spring容器调用这个方法的时候会自动传过来。我们可以直接用。

`jointPoint`方法中的`getSignature()`,获得目标方法的签名，通过方法的签名（public void generate() ）可以获取到一个方法的具体信息。





##### 切面的先后顺序

我们知道，业务流程当中不一定只有一个切面，可能有的切面控制事务，有的记录日志，有的进行安全控制，如果多个切面的话，顺序如何控制：**可以使用@Order注解来标识切面类，为@Order注解的value指定一个整数型的数字，数字越小，优先级越高**。

``` java
//另外一个切面类
package com.powernode.spring6.service;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.*;
import org.springframework.core.annotation.Order;
import org.springframework.stereotype.Component;

@Aspect
@Component
@Order(1) //设置优先级
public class YourAspect {

    @Around("execution(* com.powernode.spring6.service.OrderService.*(..))")
    public void aroundAdvice(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
        System.out.println("YourAspect环绕通知开始");
        // 执行目标方法。
        proceedingJoinPoint.proceed();
        System.out.println("YourAspect环绕通知结束");
    }

    @Before("execution(* com.powernode.spring6.service.OrderService.*(..))")
    public void beforeAdvice(){
        System.out.println("YourAspect前置通知");
    }

    @AfterReturning("execution(* com.powernode.spring6.service.OrderService.*(..))")
    public void afterReturningAdvice(){
        System.out.println("YourAspect后置通知");
    }

    @AfterThrowing("execution(* com.powernode.spring6.service.OrderService.*(..))")
    public void afterThrowingAdvice(){
        System.out.println("YourAspect异常通知");
    }

    @After("execution(* com.powernode.spring6.service.OrderService.*(..))")
    public void afterAdvice(){
        System.out.println("YourAspect最终通知");
    }
}
```

``` java
package com.powernode.spring6.service;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.*;
import org.springframework.core.annotation.Order;
import org.springframework.stereotype.Component;

// 切面类
@Component
@Aspect
@Order(2) //设置优先级
public class MyAspect {

    @Around("execution(* com.powernode.spring6.service.OrderService.*(..))")
    public void aroundAdvice(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
        System.out.println("环绕通知开始");
        // 执行目标方法。
        proceedingJoinPoint.proceed();
        System.out.println("环绕通知结束");
    }

    @Before("execution(* com.powernode.spring6.service.OrderService.*(..))")
    public void beforeAdvice(){
        System.out.println("前置通知");
    }

    @AfterReturning("execution(* com.powernode.spring6.service.OrderService.*(..))")
    public void afterReturningAdvice(){
        System.out.println("后置通知");
    }

    @AfterThrowing("execution(* com.powernode.spring6.service.OrderService.*(..))")
    public void afterThrowingAdvice(){
        System.out.println("异常通知");
    }

    @After("execution(* com.powernode.spring6.service.OrderService.*(..))")
    public void afterAdvice(){
        System.out.println("最终通知");
    }

}
```

执行测试程序：

![img](https://cdn.nlark.com/yuque/0/2022/png/21376908/1665893738167-b3c55a19-6129-4615-813f-9b8dc0f17f40.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_28%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)

通过修改@Order注解的整数值来切换顺序，执行测试程序：

![img](https://cdn.nlark.com/yuque/0/2022/png/21376908/1665893833282-2cbc59cc-15a5-44c4-bb20-cbdac65a750d.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_28%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)







##### 优化使用切点表达式



现在使用的方式缺点是：

- 第一：切点表达式重复写了多次，没有得到复用。
- 第二：如果要修改切点表达式，需要修改多处，难维护。

可以这样做：将切点表达式单独的定义出来，在需要的位置引入即可。如下：

``` java
package com.powernode.spring6.service;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.*;
import org.springframework.core.annotation.Order;
import org.springframework.stereotype.Component;

// 切面类
@Component
@Aspect
@Order(2)
public class MyAspect {
    
    @Pointcut("execution(* com.powernode.spring6.service.OrderService.*(..))")
    public void pointcut(){}

    @Around("pointcut()")
    public void aroundAdvice(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {
        System.out.println("环绕通知开始");
        // 执行目标方法。
        proceedingJoinPoint.proceed();
        System.out.println("环绕通知结束");
    }

    @Before("pointcut()")
    public void beforeAdvice(){
        System.out.println("前置通知");
    }

    @AfterReturning("pointcut()")
    public void afterReturningAdvice(){
        System.out.println("后置通知");
    }

    @AfterThrowing("pointcut()")
    public void afterThrowingAdvice(){
        System.out.println("异常通知");
    }

    @After("pointcut()")
    public void afterAdvice(){
        System.out.println("最终通知");
    }

}
```

使用@Pointcut注解来定义独立的切点表达式。

注意这个@Pointcut注解标注的方法随意，并且方法中不需要写代码，只是起到一个能够让@Pointcut注解编写的位置。

如果是想跨类使用这个定义的切点表达式就需要写包名。



### AOP中额外扩展



#### `Signature`类

Signature是 Java 反射 API 中的一个接口，用于描述方法或构造函数的签名信息。Spring AOP 中的 JoinPoint 接口继承了反射 API 中的 Member 接口，因此可以通过 JoinPoint 对象获取到方法或构造函数的 Signature 对象。

在 Spring AOP 中，切面可以通过 JoinPoint 对象获取到连接点的相关信息，其中包括方法签名信息，可以通过 JoinPoint 对象的 getSignature() 方法获取到 Signature 对象。如果连接点是一个方法，那么可以将 Signature 对象转换为 MethodSignature 对象，通过 MethodSignature 对象可以获取到更加详细的方法签名信息，比如方法返回类型、参数类型等。
在 Spring AOP 中，JoinPoint 是连接点的表示，表示在程序执行过程中的特定点，比如方法调用、异常抛出等。JoinPoint 接口定义了许多方法，可以获取连接点的相关信息，其中 getSignature() 方法可以获取连接点处的方法签名信息。
Signature 接口是一个标记接口，它没有定义任何方法。但在其子接口 MethodSignature 中，定义了 getName() 方法，用于获取方法的名称。
MethodSignature 表示方法的签名信息，包括方法名称、返回类型、参数类型等。它定义了一些方法，可以获取方法的相关信息，包括 getName() 方法用于获取方法名称、getReturnType() 方法用于获取方法返回类型、getParameterTypes() 方法用于获取方法参数类型列表等。
例如，假设有一个名为 foo 的方法，可以使用以下代码获取它的签名信息：

``` java
@Aspect
@Component
public class MyAspect {
    @Before("execution(* com.example.service.SomeService.foo(..))")
    public void before(JoinPoint joinPoint) {
        Signature signature = joinPoint.getSignature();
        if (signature instanceof MethodSignature) {
            MethodSignature methodSignature = (MethodSignature) signature;
            String methodName = methodSignature.getName();
            Class<?> returnType = methodSignature.getReturnType();
            Class<?>[] parameterTypes = methodSignature.getParameterTypes();
            // ...
        }
    }
}
```



在上面的例子中，我们使用 getSignature() 方法获取连接点的方法签名信息，然后判断签名是否为 MethodSignature 类型，如果是，就可以使用 MethodSignature 的 getName() 方法获取方法名称，getReturnType() 方法获取方法返回类型，getParameterTypes() 方法获取方法参数类型列表等。
除了 MethodSignature，还有另一个子接口 ConstructorSignature，用于表示构造函数的签名信息。
通过在 Spring AOP 中使用 JoinPoint 和 Signature 对象，我们可以获取方法或构造函数的签名信息，进而获取方法名称、返回类型、参数类型等相关信息，以便实现更加灵活的切面编程。







## Spring对事务的支持



### Spring事务管理API

Spring对事务的管理底层实现方式是基于AOP实现的。采用AOP的方式进行了封装。所以Spring专门针对事务开发了一套API，API的核心接口如下：

![img](https://cdn.nlark.com/yuque/0/2022/png/21376908/1666504216275-1b6a9ac4-6958-4cdf-9323-7a79a08d059d.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_16%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)

PlatformTransactionManager接口：spring事务管理器的核心接口。在**Spring6**中它有两个实现：

- DataSourceTransactionManager：支持JdbcTemplate、MyBatis、Hibernate等事务管理。
- JtaTransactionManager：支持分布式事务管理。

如果要在Spring6中使用JdbcTemplate，就要使用DataSourceTransactionManager来管理事务。（Spring内置写好了，可以直接用。）



### 声明式事务之注解实现方式

- 第一步：在spring配置文件中配置事务管理器。

```xml
<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
  <property name="dataSource" ref="dataSource"/>
</bean>
```

- 第二步：在spring配置文件中引入tx命名空间。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                           http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd">
```

- 第三步：在spring配置文件中配置“事务注解驱动器”，开始注解的方式控制事务。

```xml
<tx:annotation-driven transaction-manager="transactionManager"/>
```

- 第四步：在service类上或方法上添加@Transactional注解

在类上添加该注解，该类中所有的方法都有事务。在某个方法上添加该注解，表示只有这个方法使用事务。

``` java
package com.powernode.bank.service.impl;

import com.powernode.bank.dao.AccountDao;
import com.powernode.bank.pojo.Account;
import com.powernode.bank.service.AccountService;
import jakarta.annotation.Resource;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

/**
 * @author 动力节点
 * @version 1.0
 * @className AccountServiceImpl
 * @since 1.0
 **/
@Service("accountService")
@Transactional
public class AccountServiceImpl implements AccountService {

    @Resource(name = "accountDao")
    private AccountDao accountDao;

    @Override
    public void transfer(String fromActno, String toActno, double money) {
        // 查询账户余额是否充足
        Account fromAct = accountDao.selectByActno(fromActno);
        if (fromAct.getBalance() < money) {
            throw new RuntimeException("账户余额不足");
        }
        // 余额充足，开始转账
        Account toAct = accountDao.selectByActno(toActno);
        fromAct.setBalance(fromAct.getBalance() - money);
        toAct.setBalance(toAct.getBalance() + money);
        int count = accountDao.update(fromAct);

        // 模拟异常
        String s = null;
        s.toString();

        count += accountDao.update(toAct);
        if (count != 2) {
            throw new RuntimeException("转账失败，请联系银行");
        }
    }
}
```







### 事务属性包括哪些？

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21376908/1666506552984-8a4f9d42-73ba-4ded-853d-564d27340db5.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_24%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10%2Fformat%2Cwebp)

事务中的重点属性：

- 事务传播行为
- 事务隔离级别
- 事务超时
- 只读事务
- 设置出现哪些异常回滚事务
- 设置出现哪些异常不回滚事务





#### 事务的传播行为

什么是事务的传播行为？

在service类中有a()方法和b()方法，a()方法上有事务，b()方法上也有事务，当a()方法执行过程中调用了b()方法，事务是如何传递的？合并到一个事务里？还是开启一个新的事务？这就是事务传播行为。

事务传播行为在spring框架中被定义为枚举类型：

![img](https://cdn.nlark.com/yuque/0/2022/png/21376908/1666505960049-06173489-15fc-4d16-94f3-1a9025f85d8c.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_20%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)

一共有七种传播行为：

- REQUIRED：支持当前事务，如果不存在就新建一个(默认)**【没有就新建，有就加入，就是使用同一个事务】**
- SUPPORTS：支持当前事务，如果当前没有事务，就以非事务方式执行**【有就加入，没有就不管了】**
- MANDATORY：必须运行在一个事务中，如果当前没有事务正在发生，将抛出一个异常**【有就加入，没有就抛异常】**
- REQUIRES_NEW：开启一个新的事务，如果一个事务已经存在，则将这个存在的事务挂起**【不管有没有，直接开启一个新事务，开启的新事务和之前的事务不存在嵌套关系，之前事务被挂起】**
- NOT_SUPPORTED：以非事务方式运行，如果有事务存在，挂起当前事务**【不支持事务，存在就挂起】**
- NEVER：以非事务方式运行，如果有事务存在，抛出异常**【不支持事务，存在就抛异常】**
- NESTED：如果当前正有一个事务在进行中，则该方法应当运行在一个嵌套式事务中。被嵌套的事务可以独立于外层事务进行提交或回滚。如果外层事务不存在，行为就像REQUIRED一样。**【有事务的话，就在这个事务里再嵌套一个完全独立的事务，嵌套的事务可以独立的提交和回滚。没有事务就和REQUIRED一样。】**

在代码中设置事务的传播行为：

``` java
@Transactional(propagation = Propagation.REQUIRED)
```



#### 事务的隔离级别

一般用于读数据时的方法设置事务隔离级别。

事务隔离级别类似于教室A和教室B之间的那道墙，隔离级别越高表示墙体越厚。隔音效果越好。

数据库中读取数据存在的三大问题：（三大读问题）

- **脏读：读取到没有提交到数据库的数据，叫做脏读。**
- **不可重复读：在同一个事务当中，第一次和第二次读取的数据不一样。**
- **幻读：读到的数据是假的。**

事务隔离级别包括四个级别（DEFAULT级别是默认的，可以忽略）：

- 读未提交：READ_UNCOMMITTED

- 这种隔离级别，存在脏读问题，所谓的脏读(dirty read)表示能够读取到其它事务未提交的数据。

- 读提交：READ_COMMITTED

- 解决了脏读问题，其它事务提交之后才能读到，但存在不可重复读问题。

- 可重复读：REPEATABLE_READ

- 解决了不可重复读，可以达到可重复读效果，只要当前事务不结束，读取到的数据一直都是一样的。但存在幻读问题。

- 序列化：SERIALIZABLE

- 解决了幻读问题，事务排队执行。不支持并发。

**ORACLE数据库默认的事务隔离级别是第二档（READ_COMMITTED级别），MYSQL数据库默认的事务隔离级别是第三档（REPEATABLE_READ级别）**

大家可以通过一个表格来记忆：

| **隔离级别** | **脏读** | **不可重复读** | **幻读** |
| ------------ | -------- | -------------- | -------- |
| 读未提交     | **有**   | **有**         | **有**   |
| 读提交       | 无       | **有**         | **有**   |
| 可重复读     | 无       | 无             | **有**   |
| 序列化       | 无       | 无             | 无       |

在Spring代码中如何设置隔离级别？

**隔离级别在spring中以枚举类型存在：**

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21376908/1666508609641-2c838566-7334-4cf1-b452-0fed9aaebf3d.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_11%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10%2Fformat%2Cwebp)

``` java
@Transactional(isolation = Isolation.READ_COMMITTED)
```





#### 事务超时

代码如下：

``` java
@Transactional(timeout = 10)
```

以上代码表示设置事务的超时时间为10秒。

**表示超过10秒如果该事务中所有的DML语句还没有执行完毕的话，最终结果会选择回滚。**

默认值-1，表示没有时间限制。

**这里有个坑，事务的超时时间指的是哪段时间？**

**在当前事务当中，最后一条DML语句执行之前的时间。如果最后一条DML语句后面很有很多业务逻辑，这些业务代码执行的时间不被计入超时时间。**

``` java
//以下代码的超时时间不会计入超时时间
@Transactional(timeout = 10) // 设置事务超时时间为10秒。
public void save(Account act) {
    accountDao.insert(act);
    // 睡眠一会
    try {
        Thread.sleep(1000 * 15);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}
```

``` java
//以下代码的超时时间会计入超时时间
@Transactional(timeout = 10) // 设置事务超时时间为10秒。
public void save(Account act) {
    // 睡眠一会
    try {
        Thread.sleep(1000 * 15);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    accountDao.insert(act);
}
```

**当然，如果想让整个方法的所有代码都计入超时时间的话，可以在方法最后一行添加一行无关紧要的DML语句。**





#### 只读事务

代码如下：

``` java
@Transactional(readOnly = true)
```

将当前事务设置为只读事务，在该事务执行过程中只允许select语句执行，delete insert update均不可执行。

该特性的作用是：**启动spring的优化策略。提高select语句执行效率。**

如果该事务中确实没有增删改操作，建议设置为只读事务。





#### 设置哪些异常回滚事务

代码如下：

```java
@Transactional(rollbackFor = RuntimeException.class)
```

表示只有发生RuntimeException异常或该异常的子类异常才回滚。





#### 设置哪些异常不回滚事务

代码如下：

```java
@Transactional(noRollbackFor = NullPointerException.class)
```

表示发生NullPointerException或该异常的子类异常不回滚，其他异常则回滚。





### 事务的全注解式开发

编写一个类来代替配置文件，代码如下：

``` java
package com.powernode.bank;

import com.alibaba.druid.pool.DruidDataSource;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.datasource.DataSourceTransactionManager;
import org.springframework.transaction.annotation.EnableTransactionManagement;

import javax.sql.DataSource;

/**
 * @author 动力节点
 * @version 1.0
 * @className Spring6Config
 * @since 1.0
 **/
@Configuration
@ComponentScan("com.powernode.bank")
@EnableTransactionManagement
public class Spring6Config {

    //Spring框架看到这个@Bean注解之后，会调用这个方法，这个方法的返回值是一个java对象，这个java对象会自动纳入IoC容器管理
    //返回的对象就是Spring容器中的一个Bean了
    @Bean
    public DataSource getDataSource(){
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
        dataSource.setUrl("jdbc:mysql://localhost:3306/spring6");
        dataSource.setUsername("root");
        dataSource.setPassword("root");
        return dataSource;
    }

    @Bean(name = "jdbcTemplate")
    public JdbcTemplate getJdbcTemplate(DataSource dataSource){//Spring容器在调用这个方法的时候会自动传入一个dataSource对象
        JdbcTemplate jdbcTemplate = new JdbcTemplate();
        jdbcTemplate.setDataSource(dataSource);
        return jdbcTemplate;
    }

    @Bean
    public DataSourceTransactionManager getDataSourceTransactionManager(DataSource dataSource){
        DataSourceTransactionManager dataSourceTransactionManager = new DataSourceTransactionManager();
        dataSourceTransactionManager.setDataSource(dataSource);
        return dataSourceTransactionManager;
    }

}
```









## Spring集成MyBatis



### 实现步骤

#### 第一步：准备数据库表

- 使用t_act表（账户表）

#### 第二步：IDEA中创建一个模块，并引入依赖

- spring-context

- spring-jdbc

- mysql驱动

- mybatis

- mybatis-spring：**mybatis提供的与spring框架集成的依赖**

- 德鲁伊连接池

- junit

#### 第三步：基于三层架构实现，所以提前创建好所有的包

- com.powernode.bank.mapper

- com.powernode.bank.service

- com.powernode.bank.service.impl

- com.powernode.bank.pojo

#### 第四步：编写pojo

- Account，属性私有化，提供公开的setter getter和toString。

#### 第五步：编写mapper接口

- AccountMapper接口，定义方法，这里是不需要写实现类的，只用写接口，实现类是动态生成的。

#### 第六步：编写mapper配置文件

- 在配置文件中配置命名空间，以及每一个方法对应的sql。

#### 第七步：编写service接口和service接口实现类

- AccountService

- AccountServiceImpl

#### 第八步：编写jdbc.properties配置文件

- 数据库连接池相关信息

#### 第九步：编写mybatis-config.xml配置文件

- 该文件可以没有，大部分的配置可以转移到spring配置文件中。

- 如果遇到mybatis相关的系统级配置，还是需要这个文件。

#### 第十步：编写spring.xml配置文件

组件扫描

引入外部的属性文件

数据源

SqlSessionFactoryBean配置

- 注入mybatis核心配置文件路径

- 指定别名包

- 注入数据源

Mapper扫描配置器

- 指定扫描的包

事务管理器DataSourceTransactionManager

- 注入数据源

启用事务注解

- 注入事务管理器

#### 第十一步：编写测试程序，并添加事务，进行测试





### 具体实现

- 第一步：准备数据库表

连接数据库的工具有很多，除了之前我们使用的navicat for mysql之外，也可以使用IDEA工具自带的DataBase插件。可以根据下图提示自行配置：

![img](https://cdn.nlark.com/yuque/0/2022/png/21376908/1666659555476-977c1aec-6bcb-4b2b-a5d1-932a8b66cbac.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_14%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)

![img](https://cdn.nlark.com/yuque/0/2022/png/21376908/1666659459681-56e377a7-3b9e-4649-b29d-9da3c81fe46f.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_11%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)

- 第二步：IDEA中创建一个模块，并引入依赖

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.powernode</groupId>
    <artifactId>spring6-016-sm</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>

    <!--仓库-->
    <repositories>
        <!--spring里程碑版本的仓库-->
        <repository>
            <id>repository.spring.milestone</id>
            <name>Spring Milestone Repository</name>
            <url>https://repo.spring.io/milestone</url>
        </repository>
    </repositories>

    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>6.0.0-M2</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>6.0.0-M2</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.30</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.11</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>2.0.7</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.2.13</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

</project>
```

- 第三步：基于三层架构实现，所以提前创建好所有的包

![img](https://cdn.nlark.com/yuque/0/2022/png/21376908/1666660021872-5935b222-7e72-41d9-a9e1-c532ca29ef10.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_11%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)

- 第四步：编写pojo

```java
package com.powernode.bank.pojo;

/**
 * @author 动力节点
 * @version 1.0
 * @className Account
 * @since 1.0
 **/
public class Account {
    private String actno;
    private Double balance;

    @Override
    public String toString() {
        return "Account{" +
                "actno='" + actno + '\'' +
                ", balance=" + balance +
                '}';
    }

    public Account() {
    }

    public Account(String actno, Double balance) {
        this.actno = actno;
        this.balance = balance;
    }

    public String getActno() {
        return actno;
    }

    public void setActno(String actno) {
        this.actno = actno;
    }

    public Double getBalance() {
        return balance;
    }

    public void setBalance(Double balance) {
        this.balance = balance;
    }
}
```

- 第五步：编写mapper接口

```java
package com.powernode.bank.mapper;

import com.powernode.bank.pojo.Account;

import java.util.List;

/**
 * @author 动力节点
 * @version 1.0
 * @className AccountMapper
 * @since 1.0
 **/
public interface AccountMapper {

    /**
     * 保存账户
     * @param account
     * @return
     */
    int insert(Account account);

    /**
     * 根据账号删除账户
     * @param actno
     * @return
     */
    int deleteByActno(String actno);

    /**
     * 修改账户
     * @param account
     * @return
     */
    int update(Account account);

    /**
     * 根据账号查询账户
     * @param actno
     * @return
     */
    Account selectByActno(String actno);

    /**
     * 获取所有账户
     * @return
     */
    List<Account> selectAll();
}
```

- 第六步：编写mapper配置文件

一定要注意，按照下图提示创建这个目录。注意是斜杠不是点儿。在resources目录下新建。并且要和Mapper接口包对应上。

![img](https://cdn.nlark.com/yuque/0/2022/png/21376908/1666660299388-b2e278e1-497d-4357-835c-ca95bfd87f0e.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_15%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)

如果接口叫做AccountMapper，配置文件必须是AccountMapper.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.powernode.bank.mapper.AccountMapper">
    <insert id="insert">
        insert into t_act values(#{actno}, #{balance})
    </insert>
    <delete id="deleteByActno">
        delete from t_act where actno = #{actno}
    </delete>
    <update id="update">
        update t_act set balance = #{balance} where actno = #{actno}
    </update>
    <select id="selectByActno" resultType="Account">
        select * from t_act where actno = #{actno}
    </select>
    <select id="selectAll" resultType="Account">
        select * from t_act
    </select>
</mapper>
```

- 第七步：编写service接口和service接口实现类

注意编写的service实现类纳入IoC容器管理：

```java
package com.powernode.bank.service;

import com.powernode.bank.pojo.Account;

import java.util.List;

/**
 * @author 动力节点
 * @version 1.0
 * @className AccountService
 * @since 1.0
 **/
public interface AccountService {
    /**
     * 开户
     * @param act
     * @return
     */
    int save(Account act);

    /**
     * 根据账号销户
     * @param actno
     * @return
     */
    int deleteByActno(String actno);

    /**
     * 修改账户
     * @param act
     * @return
     */
    int update(Account act);

    /**
     * 根据账号获取账户
     * @param actno
     * @return
     */
    Account getByActno(String actno);

    /**
     * 获取所有账户
     * @return
     */
    List<Account> getAll();

    /**
     * 转账
     * @param fromActno
     * @param toActno
     * @param money
     */
    void transfer(String fromActno, String toActno, double money);
}
package com.powernode.bank.service.impl;

import com.powernode.bank.mapper.AccountMapper;
import com.powernode.bank.pojo.Account;
import com.powernode.bank.service.AccountService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

/**
 * @author 动力节点
 * @version 1.0
 * @className AccountServiceImpl
 * @since 1.0
 **/
@Transactional
@Service("accountService")
public class AccountServiceImpl implements AccountService {

    @Autowired
    private AccountMapper accountMapper;

    @Override
    public int save(Account act) {
        return accountMapper.insert(act);
    }

    @Override
    public int deleteByActno(String actno) {
        return accountMapper.deleteByActno(actno);
    }

    @Override
    public int update(Account act) {
        return accountMapper.update(act);
    }

    @Override
    public Account getByActno(String actno) {
        return accountMapper.selectByActno(actno);
    }

    @Override
    public List<Account> getAll() {
        return accountMapper.selectAll();
    }

    @Override
    public void transfer(String fromActno, String toActno, double money) {
        Account fromAct = accountMapper.selectByActno(fromActno);
        if (fromAct.getBalance() < money) {
            throw new RuntimeException("余额不足");
        }
        Account toAct = accountMapper.selectByActno(toActno);
        fromAct.setBalance(fromAct.getBalance() - money);
        toAct.setBalance(toAct.getBalance() + money);
        int count = accountMapper.update(fromAct);
        count += accountMapper.update(toAct);
        if (count != 2) {
            throw new RuntimeException("转账失败");
        }
    }
}
```

- 第八步：编写jdbc.properties配置文件

放在类的根路径下

```properties
jdbc.driver=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/spring6
jdbc.username=root
jdbc.password=root
```

- 第九步：编写mybatis-config.xml配置文件

放在类的根路径下，只开启日志，其他配置到spring.xml中。

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <settings>
        <setting name="logImpl" value="STDOUT_LOGGING"/>
    </settings>
</configuration>
```

- 第十步：编写spring.xml配置文件

**注意：当你在spring.xml文件中直接写标签内容时，IDEA会自动给你添加命名空间**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context" xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd">
  
    <!--组件扫描-->
    <context:component-scan base-package="com.powernode.bank"/>
  
    <!--外部属性配置文件-->
    <context:property-placeholder location="jdbc.properties"/>

    <!--数据源-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${jdbc.driver}"/>
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>

    <!--SqlSessionFactoryBean-->
    <bean class="org.mybatis.spring.SqlSessionFactoryBean">
        <!--mybatis核心配置文件路径-->
        <property name="configLocation" value="mybatis-config.xml"/>
        <!--注入数据源-->
        <property name="dataSource" ref="dataSource"/>
        <!--起别名-->
        <property name="typeAliasesPackage" value="com.powernode.bank.pojo"/>
    </bean>

    <!--Mapper扫描器，为对应的Mapper生成代理类-->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <property name="basePackage" value="com.powernode.bank.mapper"/>
    </bean>

    <!--事务管理器-->
    <bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"/>
    </bean>

    <!--开启事务注解-->
    <tx:annotation-driven transaction-manager="txManager"/>

</beans>
```

- 第十一步：编写测试程序，并添加事务，进行测试

```java
package com.powernode.spring6.test;

import com.powernode.bank.service.AccountService;
import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

/**
 * @author 动力节点
 * @version 1.0
 * @className SMTest
 * @since 1.0
 **/
public class SMTest {

    @Test
    public void testSM(){
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("spring.xml");
        AccountService accountService = applicationContext.getBean("accountService", AccountService.class);
        try {
            accountService.transfer("act-001", "act-002", 10000.0);
            System.out.println("转账成功");
        } catch (Exception e) {
            e.printStackTrace();
            System.out.println("转账失败");
        }
    }

}
```

**最后大家别忘了测试事务！！！！**



### Spring配置文件的import

spring配置文件有多个，并且可以在spring的核心配置文件中使用import进行引入，我们可以将组件扫描单独定义到一个配置文件中，如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <!--组件扫描-->
    <context:component-scan base-package="com.powernode.bank"/>

</beans>
```

然后在核心配置文件中引入：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context" xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd">

    <!--引入其他的spring配置文件-->
    <import resource="common.xml"/>

</beans>
```

**注意：在实际开发中，service单独配置到一个文件中，dao单独配置到一个文件中，然后在核心配置文件中引入，养成好习惯。**







## Spring中的八大模式

### 1 .简单工厂模式

BeanFactory的getBean()方法，通过唯一标识来获取Bean对象。是典型的简单工厂模式（静态工厂模式）；



### 2 .工厂方法模式

FactoryBean是典型的工厂方法模式。在配置文件中通过factory-method属性来指定工厂方法，该方法是一个实例方法。



### 3.单例模式

Spring用的是双重判断加锁的单例模式。请看下面代码，我们之前讲解Bean的循环依赖的时候见过：

![img](https://cdn.nlark.com/yuque/0/2022/png/21376908/1666663352271-4ba8d737-1e32-4f0e-b01a-aa305ad3abea.png?x-oss-process=image%2Fwatermark%2Ctype_d3F5LW1pY3JvaGVp%2Csize_34%2Ctext_5Yqo5Yqb6IqC54K5%2Ccolor_FFFFFF%2Cshadow_50%2Ct_80%2Cg_se%2Cx_10%2Cy_10)



### 4.代理模式

Spring的AOP就是使用了动态代理实现的。



### 5 .装饰器模式

JavaSE中的IO流是非常典型的装饰器模式。

Spring 中配置 DataSource 的时候，这些dataSource可能是各种不同类型的，比如不同的数据库：Oracle、SQL Server、MySQL等，也可能是不同的数据源：比如apache 提供的org.apache.commons.dbcp.BasicDataSource、spring提供的org.springframework.jndi.JndiObjectFactoryBean等。

这时，能否在尽可能少修改原有类代码下的情况下，做到动态切换不同的数据源？此时就可以用到装饰者模式。

Spring根据每次请求的不同，将dataSource属性设置成不同的数据源，以到达切换数据源的目的。

**Spring中类名中带有：Decorator和Wrapper单词的类，都是装饰器模式。**



### 6 .观察者模式

定义对象间的一对多的关系，当一个对象的状态发生改变时，所有依赖于它的对象都得到通知并自动更新。Spring中观察者模式一般用在listener的实现。

Spring中的事件编程模型就是观察者模式的实现。在Spring中定义了一个ApplicationListener接口，用来监听Application的事件，Application其实就是ApplicationContext，ApplicationContext内置了几个事件，其中比较容易理解的是：ContextRefreshedEvent、ContextStartedEvent、ContextStoppedEvent、ContextClosedEvent



### 7 .策略模式

策略模式是行为性模式，调用不同的方法，适应行为的变化 ，强调父类的调用子类的特性 。

getHandler是HandlerMapping接口中的唯一方法，用于根据请求找到匹配的处理器。

比如我们自己写了AccountDao接口，然后这个接口下有不同的实现类：AccountDaoForMySQL，AccountDaoForOracle。对于service来说不需要关心底层具体的实现，只需要面向AccountDao接口调用，底层可以灵活切换实现，这就是策略模式。



### 8 .模板方法模式

Spring中的JdbcTemplate类就是一个模板类。它就是一个模板方法设计模式的体现。在模板类的模板方法execute中编写核心算法，具体的实现步骤在子类中完成。















## SpringFramework



### springframework的主要的功能模块

| 功能模块       | 功能介绍                                                    |
| -------------- | ----------------------------------------------------------- |
| Core Container | 核心容器，在 Spring 环境下使用任何功能都必须基于 IOC 容器。 |
| AOP&Aspects    | 面向切面编程                                                |
| TX             | 声明式事务管理。                                            |
| Spring MVC     | 提供了面向Web应用程序的集成功能。                           |





## Spring Ioc容器



![](C:\Users\heban\Pictures\Screenshots\130011d6c79ed6ede02f83ac2dfeab30.png)

Spring IoC 容器，负责实例化、配置和组装 bean（组件）。容器通过读取配置元数据来获取有关要实例化、配置和组装组件的指令。配置元数据以 XML、Java 注解或 Java 代码形式表现。它允许表达组成应用程序的组件以及这些组件之间丰富的相互依赖关系。



Spring容器接口：

最大的接口：BeanFactory

ApplicationContext是BeanFactory的一个子接口



下面是ApplicationContext容器的实现类

| 类型名                             | 简介                                                         |
| ---------------------------------- | ------------------------------------------------------------ |
| ClassPathXmlApplicationContext     | 通过读取类路径下的 XML 格式的配置文件创建 IOC 容器对象<br />1.配置文件是xml格式<br />2.项目的类路径下，比如resources路径下 |
| FileSystemXmlApplicationContext    | 通过文件系统路径读取 XML 格式的配置文件创建 IOC 容器对象<br />1.配置文件是xml格式<br />2.文件存储到项目外，某个盘符下 c:/xx/xx.xml |
| AnnotationConfigApplicationContext | 通过读取Java配置类创建 IOC 容器对象<br />1.配置文件使用java类 |
| WebApplicationContext              | 专门为 Web 应用准备，基于 Web 环境创建 IOC 容器对象，并将对象引入存入 ServletContext 域中。 |



### 基于xml配置

#### 组件声明

基于无参构造方法

```java
//准备的组件类
package com.atguigu.ioc;

public class HappyComponent {

    //默认包含无参数构造函数

    public void doWork() {
        System.out.println("HappyComponent.doWork");
    }
}
```



```xml
<!-- 实验一 [重要]创建bean -->
<bean id="happyComponent" class="com.atguigu.ioc.HappyComponent"/>
<!-- id属性是bean的唯一标识,方便后期获取Bean
	class属性是组件类的全限定符！ 
-->
```

==要求当前组件类必须包含无参数构造函数！但是没有要求一定要是静态的==



基于静态工厂方法的实例化

```java
//准备组件类
public class ClientService {
  private static ClientService clientService = new ClientService();
  private ClientService() {}

  public static ClientService createInstance() {
  
    return clientService;
  }
}
```



编写xml文件

```xml
<bean id="clientService"
  class="examples.ClientService"
  factory-method="createInstance"/>
<!-- id属性和上面的一样
	class属性是工厂类的全限定符
	factory-method: 指定静态工厂方法，注意，该方法必须是static方法,因为是基于静态工厂方法的实例化
-->
```



基于实例工厂方法的实例化



```java
//准备组件类
public class DefaultServiceLocator {

  private static ClientServiceImplclientService = new ClientServiceImpl();

  public ClientService createClientServiceInstance() {
    return clientService;
  }
}
```



编写xml文件

```xml
<!-- 将工厂类进行ioc配置 -->
<bean id="serviceLocator" class="examples.DefaultServiceLocator">
</bean>

<!-- 根据工厂对象的实例工厂方法进行实例化组件对象 -->
<bean id="clientService"
  factory-bean="serviceLocator"
  factory-method="createClientServiceInstance"/>

<!-- factory-bean属性：指定当前容器中工厂Bean 的名称。
	factory-method:  指定实例工厂方法名。注意，实例方法必须是非static的！
-->
```



#### 组件注入依赖配置



分为基于构造函数的注入依赖和基于setter的注入依赖

> 基于构造函数的注入依赖就是在bean标签中加入<constructor-arg/>标签，这个标签有value属性，指定普通属性值，
>
> ```java
> public Person(String name){
> 	
> }
> //这里就可以使用value，就在bean双标签里加入单标签<constructor-arg value = "张三"/>
> ```
>
> 
>
> 有ref属性
>
> ```java
> class Student(){
> 	String name = "zhangsan";
> }
> 
> public Person(Student s){
> 	this.name = s.name;
> }
> 
> //这里的参数是对象，不可以用基本类型表示 
> //<bean id = "Student", class = "a.b.Student">
> //然后可以写 <bean id = "Person", class = "a.b.Person"> <constructor-arg ref = "Student"/> <bean/>
> ref属性是引用其他bean的标识（需要传入对象的标签id）
> ```

当构造方法有多个参数时可以使用name属性来指明构造方法中的参数的名字，index属性可以指明需要被赋值的参数的位置，索引从零开始，第一个参数对标索引零。



> 基于setter的注入依赖
>
> 准备组件类
>
> ```java
> public Class MovieFinder{
> 
> }
> 
> public class SimpleMovieLister {
> 
>   private MovieFinder movieFinder;
>   
>   private String movieName;
> 
>   public void setMovieFinder(MovieFinder movieFinder) {
>     this.movieFinder = movieFinder;
>   }
>   
>   public void setMovieName(String movieName){
>     this.movieName = movieName;
>   }
> 
>   // business logic that actually uses the injected MovieFinder is omitted...
> }
> ```
>
> 
>
>
> 编写xml配置文件
>
> ```xml
> <bean id="simpleMovieLister" class="examples.SimpleMovieLister">
>   <!-- setter方法，注入movieFinder对象的标识id
>        name = 属性名  ref = 引用bean的id值
>    -->
>   <property name="movieFinder" ref="movieFinder" />
> 
>   <!-- setter方法，注入基本数据类型movieName
>        name = 属性名 value= 基本类型值
>    -->
>   <property name="movieName" value="消失的她"/>
> </bean>
> 
> <bean id="movieFinder" class="examples.MovieFinder"/>
> <!-- name是需要调用的set方法的去掉set和把首字母小写的名字 set方法的方法名 -->
> ```
>
>property标签： 可以给setter方法对应的属性赋值
> property 标签： name属性代表set方法标识、ref代表引用bean的标识id、value属性代表基本属性值

==value属性和ref属性是二选一的==



## 配置文件问题

>  在Spring框架中，配置的properties等文件中，注意不要使用Spring保留的关键字

>  在Spring中，${username}并不会加载我们配置文件中些的username=xxx，而是会加载操作系统用户名。简单粗暴的方法就是username改个名字就可以了
>
> 另外，即使你足够钟意 username 这个参数名，也不能改成 userName 这样的名字。windows系统是大小写不敏感的！
>
> 但是还有另外的选择，比如：user_name 测试了一下是可以使用的
>
> 虽然但是，我选user





原文链接：https://pdai.tech/md/spring/spring-x-framework-introduce.html

