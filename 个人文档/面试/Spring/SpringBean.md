#### SpringBean的作用域
我们可以使用为`@Scope`注解来声明`Bean`的作用域。<br>

name|说明
--|--
`singleton`|唯一`Bean`实例（==默认==）
`prototype`|每次请求都会创建一个新的`Bean`实例
`request`|每一次HTTP请求都会产生一个新的`Bean`，该`Bean`仅在当前HTTP request内有效
`session`|每一次HTTP请求都会产生一个新的`Bean`，该`Bean`仅在当前HTTP session内有效

> `request`和`session`适用于WebApplicationContext

#### SpringBean单例的线程安全问题


#### `@Component`和`@Bean`


#### `@Autowired`
该注解主要用于自动装配`Bean`，要想使用该注解，需要将该注解自动装配的类，采用`@Component`、`@Repository`、`@Service`、`@Controller`。

#### Spring事务
`@Transactional`开启需要引入数据jar包
##### Spring事务传播行为
`@Transactional(propagation=传播行为 )`
- REQUIRED<br>
如果有事务在运行，当前方法就在这个方法内运行，否则，就启动一个新的事务，并早自己的事务内运行。（==默认==）
- SUPPORTS<br>
如果当前存在事务，当前方法在事务种运行，如果不存在，则以非事务方法运行
- MANDATORY<br>
如果当前存在事务，则加入该事务；如果当前没有事务，则抛出异常。
- REQUIRES_NEW<br>
当前方法必须启动一个新的事务，并在自己的事务内运行，如果有事务正在运行，应该将它挂起
- NOT_SUPPORTED<br>
以非事务方式运行，如果当前存在事务，则把当前事务挂起。
- NEVER<br>
以非事务方式运行，如果当前存在事务，则抛出异常。
- NESTED<br>
如果当前存在事务，则创建一个事务作为当前事务的嵌套事务来运行；如果当前没有事务，则该取值等价于TransactionDefinition.PROPAGATION_REQUIRED。

##### Spring事务隔离级别
`@Transactional(isolation=隔离级别 )`
- DEFAULT<br>
数据库的默认隔离级别，默认用读已提交
- READ_UNCOMMITTED（读未提交）<br>
最低隔离级别，允许读未提交，会产生脏读、幻读、不可重复读现象
- READ_COMMITTED（读已提交）<br>
允许读取并发事务已经提交的事务，防止脏读，但是依据会发生幻读、不可重复读（==常用==）
- REPEATABLE_READ（可重复读）<br>
允许对同一字段的多次提取结果是一致，除非数据是由本身事务修改，防止幻读、脏读但是不能防止不可重复读
- SERIALIZABLE（串行化）<br>
最高的隔离级别，有效防止各种错误，但是效率很低。