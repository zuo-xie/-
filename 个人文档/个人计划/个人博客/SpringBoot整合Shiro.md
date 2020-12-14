> Apache Shiro是一个强大且易用的Java安全框架,执行身份验证、授权、密码学和会话管理。相比较Spring Security，shiro有小巧、简单、易上手等的优点。所以很多框架都在使用shiro。
>Shiro包含了三个核心组件：Subject, SecurityManager 和 Realms。

1. Subject（主体）：代表当前用户的安全操作（一般指==用户==）
2. SecurityManager（安全管理器）：==Shiro框架的核心==，用来管理内部的组件实例和提供安全管理的各种服务。
3. Realms（连接器）：相当于桥梁，是Shiro和项目的桥梁，进行权限信息的验证，Shiro会从应用配置的Realm中查找用户及其权限信息。

### 使用Shiro框架

配置`pom.xml`添加依赖
```xml
        <dependency>
            <groupId>org.apache.shiro</groupId>
            <artifactId>shiro-spring</artifactId>
            <version>1.5.1</version>
        </dependency>
```
> 注意一下不要用`shiro-core`在测试的时候缺少CookieRememberMeManager
> 具体原因不清楚

