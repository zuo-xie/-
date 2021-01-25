### SpringBean
#### SpringBean的介绍
我们在使用Spring的时候经常会使用`@Autowired``@Reference`等注解去调用`@Service@Controller`等类，而这些类就是SpringBean。
SpringBean是Spring框架的基本架构块。
Bean是一个被实例化、组装、并通过SpringIOC进行管理的对象。

#### Bean容器
Spring用来存储Bean的容器有两中容器`BeanFactory（Bean工厂）`和`ApplicationContext（应用上下文）`。<br>
`ApplicationContext`是实现于`BeanFactory`。
这两种体系的关系

- `BeanFactorys实现类`属于外观模式的子系统承担着外界提供Bean对象的主要责任，是功能实现的主体
- `ApplicationContext`作为`BeanFactory实现类`的外观系统，通过`BeanFeactory`提供的接口结合具体业务
##### `BeanFactory`容器
`BeanFactory`作为Spring IOC的核心担当，其主要作用是，通过抽象Bean实例化的具体过程（`BeanDefinition`），借助依赖注入的能力，实现基于元数据的业务对象自动装配。
`BeanFactory`作为Spring的底层接口，提供了Bean的注册能力（包括Bean查询、类型判断、scope判断等基础能力）。

##### `ApplicationContext`容器
`ApplicationContext`是`BeanFactory`的子类之一，与`BeanFactory`类似，它可以加载配置文件中的Bean，将所有Bean集中在一起，当有请求的时候分配Bean。
`ApplicationContext`拥有`BeanFactory`的所有功能。

##### `Bean`的作用域
在springboot中，Bean的作用域

##### `Bean`的生命周期


> [BeanFactory，Spring IoC的核心担当](https://zhuanlan.zhihu.com/p/161401436)
> [Spring ApplicationContext 容器](https://wiki.jikexueyuan.com/project/spring/ioc-container/spring-application-context-container.html)
> [Spring Bean的生命周期（非常详细）]( http://www.cnblogs.com/zrtqsk/p/3735273.html)
