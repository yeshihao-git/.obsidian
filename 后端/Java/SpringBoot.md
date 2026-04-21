# 1. SpringBoot 核心概念

| 概念             | 类比 C++      | 说明                                 |
| -------------- | ----------- | ---------------------------------- |
| IoC 容器         | 全局对象管理器     | Spring 自动创建和管理对象（叫 Bean），不需要手动 new |
| 注解（Annotation） | 类似 C++ 属性/宏 | 以 @ 开头，给类/方法附加元数据，Spring 读取后自动配置   |
| 依赖注入（DI）       | 构造函数传参      | Spring 自动把需要的对象传给你，不用自己创建          |


# 2. SpringBoot 常用注解
## 2.1 分层标记注解

| 注解            | 归属层         | 核心含义            | 底层本质             |
| ------------- | ----------- | --------------- | ---------------- |
| `@Component`  | 通用类         | 交给Spring IOC 管理 |                  |
| `@Service`    | 业务层 Service | 业务逻辑类           | **就是@Component** |
| `@Repository` | 数据层 DAO     | 数据库操作类          | **就是@Component** |
| `@Controller` | 控制层 Web     | 接收前端请求的类        | **就是@Component** |

## 2.2 IOC & 配置相关注解

| 注解               | 作用    | 核心一句话                  |
| ---------------- | ----- | ---------------------- |
| `@Bean`          | 方法上注解 | 返回对象交给 Spring IOC 管理   |
| `@Autowired`     | 自动注入  | 自动从容器拿 Bean 赋值，不用自己new |
| `@Configuration` | 配置类注解 | 标记当前类是配置类，配合`@Bean`使用  |

## 2.3 SpringBoot 启动总注解
| 注解                       | 作用             | 内部三合一本质                                                                                 |
| ------------------------ | -------------- | --------------------------------------------------------------------------------------- |
| `@SpringBootApplication` | springboot启动入口 | 1.`@Configuration`配置<br>2.`@ComponentScan`自动扫包造Bean<br>3.`@EnableAutoConfiguration`自动配置 |

## 2.4 Web接口专用注解
| 注解 | 作用 |
|------|------|
| `@RestController` | 接口控制器（返回JSON）= `@Controller` + `@ResponseBody` |
| `@RequestMapping` | 映射接口路径 |
| `@GetMapping` | GET请求接口 |
| `@PostMapping` | POST请求接口 |

## 2.5 如何使用？
```
启动用 @SpringBootApplication
配置用 @Configuration + @Bean
组件用 @Component / @Service / @Repository / @Controller
注入用 @Autowired
Web 用 @RestController + @GetMapping/@PostMapping
WebSocket 用 @ServerEndpoint + @OnMessage
事务用 @Transactional
```