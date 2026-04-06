





## 什么是Spring Boot ？和Spring 有什么关系

> 回答思路：Spring是爹，先回答下什么是Spring
>
> Spring是一个技术生态/体系，一个轻量级的开源框架。其中就包括众多组件，Spring Boot、Spring Framework、Spring MVC、Spring Cloud等等，
>
> **如果说的不是这个Spring意思，而是 "Spring开发" 这个语义下的Spring，则就是Spring Framework。**
>
> Spring Boot 是一个基于Spring 做的 “快速启动工具”，用来简化Spring 的开发。
>
> 但是说到这又可以扩展到使用Spring Boot 的优点有哪些？

Spring是一个技术生态/体系，一个轻量级的开源框架。其中就包括众多组件，Spring Boot、Spring Framework、Spring MVC、Spring Cloud等等，

Spring Boot 是一个基于Spring 做的 “快速启动工具”，用来简化Spring 的开发。





## 使用Spring Boot 有哪些优点？为什么要使用Spring Boot 进行开发？

> 把传统Spring开发和Spring Boot 开发进行比较
>
> 传统 Spring 开发：
> 	配置：大量XML文件
> 	依赖：需要一个个导包，容易冲突
> 	开发效率：低，搭建慢
> 	适用场景：传统项目、初学时使用（学习底层）
>
> 使用Spring Boot 开发：
> 	配置：极度简化、自动配置
> 	依赖：starter 统一管理
> 	开发效率：高，开箱即用
> 	适用场景：现代企业开发新项目、微服务友好

- 配置：极度简化、自动配置
- 依赖：starter 统一管理
- 开发效率：高，开箱即用
- 适用场景：现代企业开发新项目、微服务友好



## Spring Boot 怎么声明一个Bean？

> 一般都是使用注解来声明一个Bean的
> 常见的声明方式有：注解声明、XML文件声明
>
> 注解声明又分为`@Component`注解声明、`@Bean`注解声明、`@Import`注解声明
>
> 简单类声明：使用`@Component`、`@Controller`、`@Service`、`@Mapper`
>
> 第三方类 / 手动控制创建逻辑：`@Bean`
>
> 批量导入 Bean 或配置类：`@Import`

使用`@Component`注解、`@Bean`注解、`@Import`注解、XML文件声明





