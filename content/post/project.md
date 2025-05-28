---
date: '2025-03-16T20:46:31+08:00'
title: 'Project'
lastmod: 2025-03-16T20:46:31+08:00

categories:
- project


summary: "project"
layout: "project" # necessary for search

tags:
- project1

description: "" # 文章描述，与搜索优化相关
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true
showToc: true # 显示目录
TocOpen: true # 自动展开目录
autonumbering: true # 目录自动编号
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
searchHidden: false # 该页面可以被搜索到
showbreadcrumbs: true #顶部显示当前路径
mermaid: true
cover:
    image: ""
    caption: ""
    alt: ""
    relative: false
---

## 打开项目
http://localhost/
监测监听端口
curl http://127.0.0.1:80
接口文档
http://localhost:8081/doc.html#/
## nginx
```
sudo nginx # 开启
sudo nginx -s stop # 停止
#查看8081端口被什么占据
sudo lsof -i :8081
COMMAND   PID   
java    17143
#强制结束进程
kill -9 17143
```
## 日志
#### @Slf4j 
注解自动为这个类生成 log 变量，不需要手动创建。
相当于
```java
private static final org.slf4j.Logger log = org.slf4j.LoggerFactory.getLogger(EmployeeController.class);
```
然后 `log.info("new employee:" + employeeDTO) `就可以用来打印日志。
即使日志级别不输出 INFO，Java 也会拼接字符串，影响性能。而 {} 只有日志真的要打印时才会拼接字符串，性能更好。
所以使用
```java
log.info("员工信息：{}", employeeDTO); //如果 employeeDTO 是一个对象，默认会调用 employeeDTO.toString() 方法
```
## use json 
- `@RequestBody`
接收前端传递给后端的json字符串中的数据
<font color=#008000>一个请求，只有一个RequestBody</font>
- `@Post` 接口路径
- `@RequestMapping("/admin/employee")` 后面的路径信息，在使用时重新写`@RequestMapping`
- `@ApiOperation("注释信息")`API Swagger注释
## use DTO
DTO（**Data Transfer Object**，数据传输对象）封装数据，减少方法调用的次数，并避免暴露底层业务逻辑。
#### 作用
1.	只包含数据 
DTO 主要用于存储和传输数据只是一个数据容器。
2.	减少远程调用次数
在分布式系统或 Web API 设计中，DTO 可以将多个数据封装到一个对象中，从而减少远程调用时的请求次数
3.	解耦数据层和业务层
DTO 使得数据模型和业务逻辑层之间更加独立，避免直接暴露数据库实体（如 ORM 实体），提高安全性。
#### 应用：
1.	前后端交互
在 Web 开发中，后端 API 往往会返回 DTO，而不是直接返回数据库的实体类，以防止数据泄露或字段不必要地暴露。
2.	微服务架构
在微服务之间传输数据时，使用 DTO 作为数据封装对象，可以保持 API 接口的稳定性，避免不同微服务之间数据格式不兼容的问题。
      
	1.	字段名不同：
	•	旧版本 API 里字段叫 "user_id"，新版本改成了 "id"，可以用 DTO 适配。
	2.	数据结构不同：
	•	前端可能把地址作为 "address": "New York" 传过来，而后端希望拆分成 city 和 state 字段，DTO 可以做转换。
	3.	版本兼容性：
	•	旧版本 API 可能不返回某个字段，新版本增加了字段，DTO 可以确保新旧 API 兼容，不会影响老用户。
	4.   Type不同：
   	•	
3.	数据库查询优化
例如，在查询数据库时，使用 DTO 只获取需要的字段，而不是整个数据库实体，可以减少数据加载，提高查询效率。
```java
//controller中
@PostMapping
    @ApiOperation("新增员工")
    public Result save(@RequestBody EmployeeDTO employeeDTO){
        log.info("新增员工:{}", employeeDTO);
        employeeService.save(employeeDTO);
    return null;
    }
 //serviceImpl中，业务层逻辑
public void save(EmployeeDTO employeeDTO) {
        Employee employee = new Employee(); //建议使用实体类
        employee.setId(employeeDTO.getId());//so on 但是繁琐
        //copy obj's properties
        BeanUtils.copyProperties(employeeDTO, employee);
        //employee里有但是employeeDTO中无的属性
        employee.setStatus(StatusConstant.ENABLE);//自定义的常量类public class StatusConstant { public static final Integer ENABLE = 1; }
        employee.setCreateTime(LocalDateTime.now());//LocalDateTime.now() 系统目前时间
        //最后封装到数据层（持久层）
        employeeMapper.insert(employee);
```
## 微信登录 & 小程序
### HttpClient
构造发送http请求
**核心API**
HttpClient
- 发送HTTP请求
- 接收响应数据
- 是接口interface
HttpClients http构造，创建HttpClient对象
CloseableHttpClient HttpClient的impl，
HttpGet get请求
HttpPost post请求
**发送请求步骤**
create HttpClient obj -> create Http请求 obj -> use HttpClient.execute() send 请求
#### get请求
1. 创建HttpClient对象
CloseableHttpClient httpClient = HttpClients.createDefault();
2. 创建请求对象
HttpGet httpGet = new HttpGet("http://localhost/user/shop/status");
3. 发送请求，接受响应结果
CloseableHttpResponse response = **httpClient.execute**(httpGet);
4. 解析结果
int statusCode = response.getStatusLine().getStatusCode();
System.out.println("服务端返回的状态码为：" + statusCode);
HttpEntity entity = response.getEntity();
String body = EntityUtils.toString(entity);
System.out.println("服务端返回的数据为：" + body);
5. 关闭资源
response.close();
httpClient.close();
#### POST方式请求 
1. 创建HttpClient对象
2. 创建请求对象
3. 发送请求，接收响应结果
4. 解析响应结果
5. 关闭资源
## 微信小程序

