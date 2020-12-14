
> 本文只是简单介绍一些SpringBoot的常用注解，没有实际代码
>
> 后期会继续进行文档编写
>
> [ JavaGuide----接近8000字的Spring/SpringBoot常用注解总结！安排！](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247486635&idx=1&sn=9028d00727923f51240053666c9eb3a4&chksm=cea24360f9d5ca76e8afc7159c0dc463cf83adb798e68a39b2ba4f92f66971a60b70855384c4&token=714726583&lang=zh_CN#rd)

- `@SpringBootApplication`<br>
SpringBoot项目最基本以及根本的注解，默认在主类上使用。<br>
`@SpringBootApplication`是由`@Configuration`、`@EnableAutoConfig`、`@ComponentScan`三个注解的组合。<br>
三个注解的作用

注解|说明
--|--
`@Configuration`|允许在Spring·上下文中注册额外的Bean或导入其他配置类
`@EnableAutoConfig`|启用SpringBoot的自动配置机制
`@ComponentScan`|扫描被`@Component`注解的Bean，注解默认会扫描该类所在的包下的所有类

- `@Autowired`<br>
自动导入对象到类中，被注入的类接受当前类的容器管理

- `@Component`

注解|说明
--|--
`@Repository`|对应持久层（`Mapper或Dao层`）,主要用于数据库相关操作
`@Service`|对应服务层，主要涉及一些复杂的逻辑，需要使用持久层
`@Controller`|对应SpringMVC控制层，主要接收用户请求并调用服务层返回数据

- `@RestController`<br>
由`@Controller`和`@ResponseBody`的组合，表示这是一个控制器Bean，并且是将函数的返回值接入直接填入到**HTTP响应头**，是一个Rest风格的控制器
> 单独使用`@Controller`一般是在前后端不分离的情况下，适用于前后端不分离

- `@Scope`<br>
声明SpringBoot中Bean的作用域。<br>
常见的作用域：

作用域|说明
--|--
`singleton`|唯一Bean实例，Spring中的Bean默认都是单例
`prototype`|每次请求都会创建一个新的Bean实例
`request`|每一次Http请求都会产生一个新的Bean，仅在当前Http request内有效
`session`|每一次Http请求都会产生一个新的Bean，仅在当前Http session内有效

- `@Configuration`<br>
一般用于声明配置类，可以使用`@Component`注解替代，不过使用该注解更加语义化。

- `@RequestMapping`<br>
配置**url**映射。<br>
该注解可以作用在控制器上，也可以作用在控制器方法上。<br>
如果使用在方法上可以添加以下几个请求

`method`请求|说明
--|--
`GET`|请求服务器获取特定资源
`POST`|在服务器上创建一个新的资源
`PUT`|更新服务器上的资源
`DELETE`|从服务器删除特定的资源
`PATCH`|更新服务器上的资源

- `@PathVariable`<br>
获取路径参数。

- `@RequestParam`<br>
用于获取查询参数。

- `@RequestBody`<br>
主要用于接收前端传递给后端的JSON字符串。

- `@Value`<br>
读取比较简单的配置信息。

- `@ConfigurationProperties`<br>
通过该注解读取配置信息并与Bean绑定

- 常用参数校验

注解|说明
--|--
`@NotEmpty`|字符串不能为`null`，也不能为空
`@Pattern(regex=,flag=)`|元素必须符合指定的正则表达式
`@Email`|元素必须为`Email`格式
`@Min(value)`|元素必须**大于等于**指定数字
`@Max(value)`|元素必须**小于等于**指定数字
`@Size(min=,max=)`|元素必须在指定大小范围
日后再添|
> 使用这些注解必须再控制器上需要验证的参数前面加上 `@Valid`注解

- `@ControllerAdvice`<br>
注解定义全局异常处理类。

- `@Transactional`<br>
在方法上开启事务。


