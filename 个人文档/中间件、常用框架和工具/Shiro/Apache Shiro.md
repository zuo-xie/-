- `Apache Shiro`是Java的一个安全（权限）框架。
- `Shiro`可以相比`Spring security`更加便捷，不仅适用于==JavaSe==环境，也可以在==JavaEE==环境。
- Shiro的作用：
    - 认证
    - 授权
    - 加密
    - 会话管理
    - Web集成
    - 缓存

#### 功能简介
![Shiro功能简介图]()

- Authentication：身份认证/登录，验证用户是不是拥有相应的身份。
- Authorization：授权，即权限验证，验证某个已认证的用户是否拥有某个权限；即判断用户是否能做事情。
- Session Management：会话管理，即用户登录后就是一次会话，在没有退出之前，它的所有信息都会在会话中；会话可以是普通的JavaSE环境的，也可以是Web环境的。
- Cryptography：加密，保护数据的安全性，如密码加密存储到数据库，而不是明文存储。
- Web Support：Web支持，可以非常容易的集成到Web环境。
- Caching：缓存，比如用户登录后，其用户信息，拥有的角色/权限不必每次去查，这样可以提高效率。
- Concurrency：Shiro支持多线程应用的并发验证，即如在一个线程中开启另一个线程，能把权限自动传播过去。
- Testing：提供测试支持。
- "Run As"：允许一个用户假装为另一个用户（如果允许的话）的身份进行访问。
- Remember Me：记住我，这是一个非常常见的功能，即一次登录后，下次不用登录。
> 记住Shiro不会维护用户、维护权限；这些需要我们自己去设计/提供；然后通过相应的接口注入给Shiro即可。

### Shiro的架构
![Shiro的架构（对于使用者）]()

常用的Api
- Subject：代表当前正在登录的用户（将用户数据封装到Subject）。
- Shiro SecurityManager：安全管理器，Shiro的核心，==Shiro的所有组件都是由它实现的==。
- Realm：域（安全数据源），Shiro从Realm中获取安全数据（如用户、角色和权限），SecurityManager要验证用户的身份，那么它需要从Realm获取相应的用户进行比较以确定用户身份是否合法；也需要从Realm得到用户相应的角色/权限进行验证用户是否能继续操作。

### Shiro的框架
![Shiro的框架]()

