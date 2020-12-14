### MyBatis介绍
MyBatis是Apache开源的一个基于Java的持久层框架。
我们一般将它与`Spring Data JPA`进行比较。
优点：
	- 上手简单
	- 支持动态SQL编写
	- 提供XML标签
缺点
	- 对SQL有一定要求
	- 依赖于数据库，难以移植代码
	- 本身缓冲机制较差

> 这次不重点介绍JPA

### `JDBC`
> 被项目使用Maven作为版本控制器
在MyBatis等ORM框架开源之前，我们是直接利用`JDBC`去连接数据库的，所以我会先从`JDBC`开始讲解。
引入Jar包
```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.21</version>
</dependency>
```

代码编写
```java
public class JDBCTextDemo01 {
    public static void main(String[] args) throws Exception{
        String url = "jdbc:mysql://47.114.189.73:3306/user";
        String userName = "root";
        String password = "123456";
        //加载驱动程序
        Class.forName("com.mysql.cj.jdbc.Driver");
        //连接数据库
        Connection connection = DriverManager.getConnection(url, userName, password);
        //用于执行静态SQL语句
        Statement statement = connection.createStatement();
        //真正执行的SQL
        ResultSet resultSet = statement.executeQuery("select USER_ID,USER_NAME from USER ");
		//遍历输出
        while(resultSet.next()) {
        	指定相应字符串
            System.out.println(resultSet.getString("USER_NAME"));
        }

        //关闭资源，避免资源浪费
        resultSet.close();
        statement.close();
        connection.close();
    }
}
```
我们发现执行1条SQL语句的步骤需要太多，代码冗余量太大。MyBatis的出现极大的简化了这些步骤，从而让我们这些开发人员，更加注重业务逻辑的编写。
### MyBatis的使用

引入Jar包
```xml
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.0</version>
</dependency>
```

代码编写
```java

```