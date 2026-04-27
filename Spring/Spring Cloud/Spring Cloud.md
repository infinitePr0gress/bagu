# Spring Cloud 和 Spring Boot 的关系

## 定位区别

Spring Boot 的核心目标是**简化 Spring 应用的初始搭建和开发**，通过自动配置（Auto Configuration）、起步依赖（Starter）和内嵌容器，让开发者能快速跑起一个独立的、生产级别的 Spring 应用。

Spring Cloud 则是在 Spring Boot 的基础上，提供了一套**分布式系统（微服务）架构的一站式解决方案**，解决服务注册与发现、配置管理、负载均衡、熔断限流、网关路由等问题。

简单说：**Spring Boot 负责"快速开发单体应用"，Spring Cloud 负责"将多个 Boot 应用协同组成分布式系统"。**

---

## 依赖关系

Spring Cloud **完全依赖 Spring Boot**，不能独立存在：

- Spring Cloud 的每一个组件（如 Eureka、Ribbon、Feign、Hystrix、Gateway 等）都是以 Spring Boot Starter 的形式提供的
- Spring Cloud 的自动配置类，依赖 Spring Boot 的 `@EnableAutoConfiguration` 机制生效
- Spring Cloud 的版本必须与对应 Spring Boot 版本严格兼容（这是初学者最容易踩的坑）

反之不成立：Spring Boot **完全不依赖** Spring Cloud，可以独立使用。

---

## 版本兼容性

Spring Cloud 的版本命名采用"伦敦地铁站名"（如 Hoxton、2020.0.x / Ilford），每个大版本都绑定一个特定的 Spring Boot 版本范围。

| Spring Cloud 版本 | 对应 Spring Boot 版本 |
|---|---|
| 2024.0.x（Happi） | 3.4.x |
| 2023.0.x（Leyton） | 3.2.x / 3.3.x |
| 2022.0.x（Kilburn） | 3.0.x / 3.1.x |
| 2021.0.x（Jubilee） | 2.6.x / 2.7.x |
| Hoxton | 2.3.x / 2.4.x |

> ⚠️ 版本不匹配是最常见的启动报错原因之一，引入依赖前务必核对官方兼容性表。

---

## 典型协作方式

一个最基础的 Spring Cloud 微服务项目结构如下：

```
service-registry    （Eureka Server，基于 Spring Boot）
  └─ 端口 8761，负责服务注册

order-service       （Spring Boot + Spring Cloud）
  └─ 业务服务，启动时向 registry 注册自己

user-service        （Spring Boot + Spring Cloud）
  └─ 业务服务，同样注册到 registry

api-gateway         （Spring Boot + Spring Cloud Gateway）
  └─ 统一入口，路由转发、鉴权、限流
```

每个服务都是**独立的 Spring Boot 应用**，通过引入对应的 Spring Cloud Starter（如 `spring-cloud-starter-netflix-eureka-client`）获得微服务能力。
类比：Spring Boot是一块块砖，Spring Cloud是用这些砖建成的大楼。或者Spring Boot是做单个微服务的快捷方式，Spring Cloud是把这些微服务连接起来形成系统的框架。

---

## 总结一句话

> **Spring Boot 是"术"，让你快速写好一个服务；Spring Cloud 是"阵"，让多个服务协同工作。先掌握 Boot，再学 Cloud。**
