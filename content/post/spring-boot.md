
---
title: Spring Boot Web 框架学习
date: 2025-03-02
categories: [Spring Boot]
url: "/SpringBoot/"
tags: [Spring Boot, Spring Web, Web开发, REST API]
---

## 1. 为什么要使用 Spring Web？
Spring Web 是 **Spring 框架中的一个模块**，用于简化 **Web 应用开发**，特别是 **REST API 和 MVC**（Model-View-Controller）架构。使用 Spring Web 的主要原因有：
<!--more-->
✅ **简化 Web 开发**  
- 只需要少量配置，就能快速搭建 Web 应用或 RESTful API。
- 通过注解（如 `@RestController`、`@RequestMapping`）来定义 API，而不需要手写大量的 Servlet 代码。

✅ **内置服务器，开箱即用**  
- Spring Boot 提供了 **内嵌 Tomcat、Jetty 或 Undertow**，不需要额外安装服务器。
- 直接运行 Spring Boot 应用，就能启动 Web 服务。

✅ **强大的 REST 支持**  
- 轻松创建 RESTful API，支持 JSON/XML 数据格式返回。
- 内置 `RestTemplate` 和 `WebClient`，方便调用外部 API。

✅ **与 Spring 生态系统无缝集成**  
- 可以轻松结合 **Spring Security（身份验证和授权）**、**Spring Data（数据库访问）** 和 **Spring Cloud（微服务架构）**。
- 支持与前端框架（如 React、Vue.js）结合，构建前后端分离的应用。

✅ **强大的异常处理和拦截器机制**  
- 通过 `@ExceptionHandler` 统一处理异常，增强 API 可靠性。
- 可以使用 **拦截器（Interceptor）** 处理请求，例如权限验证、日志记录等。

---

## 2. 什么时候会使用 Spring Web？
Spring Web 适用于：
1. **开发 RESTful API**：  
   - 例如构建一个后端服务，提供 JSON 数据给前端（Vue、React）。
   - 适用于移动端（iOS/Android）或前后端分离的 Web 项目。

2. **传统 MVC 模式的 Web 应用**：  
   - 适用于小型到中型项目，直接用 Spring Web + Thymeleaf 渲染页面。

3. **微服务架构**：  
   - 在 Spring Cloud 中，Spring Web 常用于构建微服务，提供 HTTP API。

4. **处理 HTTP 请求，如爬虫、Webhook 监听**：
   - 例如监听 GitHub Webhook 事件，自动触发 CI/CD 流程。

---

## 3. 怎么使用 Spring Web？

### （1）引入 Spring Web 依赖
**Maven**，在 pom.xml 添加：
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```
### （2）创建 Spring Boot 主类

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
@SpringBootApplication
public class WebApplication {
    public static void main(String[] args) {
        SpringApplication.run(WebApplication.class, args);
    }
}
```
- @SpringBootApplication：Spring Boot 启动类，自动扫描组件并启动应用。

### （3）创建 REST API 控制器
```java
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api")
public class HelloController {

    @GetMapping("/hello")
    public String sayHello() {
        return "Hello, Spring Boot!";
    }

    @GetMapping("/greet/{name}")
    public String greetUser(@PathVariable String name) {
        return "Hello, " + name + "!";
    }
}
```
📌 **解释：**
- 	@RestController：标识这是一个 REST API 控制器。
-	@RequestMapping("/api")：设置 API 访问的基础路径 /api。
-	@GetMapping("/hello")：定义 GET 请求，访问 http://localhost:8080/api/hello 时返回 "Hello, Spring Boot!"。
-	@PathVariable：获取 URL 参数，例如访问 http://localhost:8080/api/greet/Alice，会返回 "Hello, Alice!"。
### （4）运行 Spring Boot 应用
在终端运行：
```bash
mvn spring-boot:run  # 使用 Maven 启动
# 或者
gradle bootRun       # 使用 Gradle 启动
```
然后打开浏览器访问：
http://localhost:8080/api/hello
返回：
```bash
Hello, Spring Boot!
```

--- 

### （5）处理 POST 请求
如果你要处理 POST 请求，可以这样做：
```java
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api")
public class UserController {

    @PostMapping("/user")
    public String createUser(@RequestBody User user) {
        return "User created: " + user.getName();
    }
}
```
其中 User 是一个普通的 Java 类：
```java
public class User {
    private String name;
    
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```
测试 POST 请求：
```bash
curl -X POST -H "Content-Type: application/json" -d '{"name": "Alice"}' http://localhost:8080/api/user
```
返回：User created: Alice

### （6）使用 RestTemplate 调用外部 API
Spring Web 还可以用来调用其他 REST API：
```java
import org.springframework.stereotype.Service;
import org.springframework.web.client.RestTemplate;

@Service
public class ApiService {
    private final RestTemplate restTemplate = new RestTemplate();

    public String getApiData() {
        String url = "https://jsonplaceholder.typicode.com/todos/1";
        return restTemplate.getForObject(url, String.class);
    }
}
```
## 总结

Spring Web 是开发 **Web 应用程序**和 RESTful API 的核心框架之一。
它简化了开发流程，并且通过内嵌服务器（如 Tomcat）提供了开箱即用的功能。
无论是构建传统的 MVC 模式应用，还是开发现代的 RESTful API，Spring Web 都能提供强大的支持。

通过使用 Spring Boot，开发者可以快速启动并运行一个 Web 应用，而不需要复杂的配置。
创建 REST API 变得更加简单，只需使用注解如 `@RestController`、`@GetMapping` 和 `@PostMapping`，
即可轻松处理各种 HTTP 请求。

✅ 使用场景
- 开发后端 API，提供 JSON 数据。
- 创建前后端分离的 Web 应用。
- 支持微服务架构；

✅ 使用步骤：

	1.引入 spring-boot-starter-web 依赖。
	2.创建 @SpringBootApplication 主类。
	3.使用 @RestController 定义 API。
	4.运行 Spring Boot 应用并测试 API。
