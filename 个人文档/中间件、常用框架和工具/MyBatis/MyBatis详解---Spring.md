### `SqlSessionFactoryBean`
在基础的MyBatis语法中，`SqlSessionFactory`是由`SqlSessionFactoryBulid`创建的，而在MyBatis-Spring中是由`SqlSessionFactoryBean`创建的。<br>
由于该类实现了`FactoryBean`方法，该类最终会将`getObject()`方法的返回值，也就是 `SqlSessionFactory`注入到`Spring`容器中。<br>
核心属性解析：<br>
- `configLocation`：用来指定MyBatis的配置文件路径
- `sqlSessionFactory`：用于JDBC的`DataSource`
- `dataSource`：用于连接数据库的数据源
- `mapperLocations`：mapper文件存放的位置
- `typeAliasesPackage`：对应实体类所在的包
- `configuration`：MyBatis配置属性
- `sqlSessionFactoryBuilder`：对应的sqlSessionFactory创建器

方法解析：<br>
- `afterPropertiesSet()`
由`SqlSessionFactoryBean`实现的接口`InitializingBean`提供，该方法在初始化Bean的时候执行，该方法主要获取`SqlSessionFactory`。
首先会去判断`dataShource`、`sqlSessionFactoryBuilder`、`configLocation`和`configuration`。
然后调用`buildSqlSessionFactory()`方法