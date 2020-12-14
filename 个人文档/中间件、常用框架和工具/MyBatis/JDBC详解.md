### `JDBC`介绍

之前我说过无论是`MyBatis`还是`Spring Data JPA`底层都是封装了`JDBC`，那`JDBC`是什么。

`JDBC`等同于`Java Data Base Connectivity`（Java数据库连接），是一个操作数据库语句的API。是由SUN公司制定的，不过SUN公司只是去设置了相应规定，具体的实现由各个数据库公司去制定。

### `JDBC`的使用

```java
public class JDBCTextDemo01 {
    public static void main(String[] args) throws Exception{
        String url = "";
        String userName = "";
        String password = "";
        //加载驱动程序
        //根据不同的需求操作不同的数据库
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

### `JDBC`相关接口介绍
#### `Connection`
与特定数据库连接，执行SQL语句，并在连接的上下文中返回结果。
可通过`getMetaData`来获取对应数据库的信息。
配置连接时，应使用适当的连接方式。如果JDBC的方法可用，则以JDBC中的方法去修改配置，不应直接使用SQL语句修改。
默认情况下，该对象处于自动提交，表示它在执行每个语句之后会自动提交。如果禁用，则必须调用相应方法，否则不会在数据库中保存。（这里指事务）

> 注释我并没有写完，剩下的部分，我还不是特别理解。可以自行去查看。


事务|具体说明
--|--
`TRANSACTION_NONE`|不支持事务
`TRANSACTION_READ_COMMITTED`|读未提交
`TRANSACTION_READ_UNCOMMITTED`|不可重复读
`TRANSACTION_REPEATABLE_READ`|可重复读
`TRANSACTION_SERIALIZABLE`|串行化

> 这里的事务，是SQL事务的隔离级别，这个自行查看。

常用方法|说明
--|--
`void close()`|立即释放`connection`对象的数据库和`JDBC`资源，而不是等待它们被自动释放
`void commit()`|提交所有更改内容并释放该`connection`对象锁定的资源
`void setAutoCommit()`|设置此`Connection`对象的自动提交模式    
`Statement createStatement()`|创建一个`Statement`对象来封装`SQL`并发送给数据库
`CallableStatement prepareCall()`|创建一个`CallableStatement`对象来封装`SQL`并调用数据库
`PreparedStamtement prepareStatement()`|创建一个`PreparedStatement`对象，用于将封装`SQL`并调用
`void rollback()`|取消在当前事务进行的所有更改，并释放该对象目前持有的锁

###### `Statement`
用于执行静态`SQL`语句并返回其产生的结果的对象。
默认情况下，每个`Statement`对象只能同时打开一个`ResultSet`对象。因此，如果一个`ResultSet`对象的读取与另一个对象的读取交错，则每个都必须由不同的`Statement`对象生成。如果存在打开的语句，`Statement`接口中的所有执行方法都会隐式关闭该语句的当前`ResultSet`对象

常用方法|说明
--|--
`ResultSet executeQuery()`|执行给定的`SQL`语句，该语句返回一个`ResultSet`对象,用于查询
`int executeUpdate()`|执行指定的`SQL`语句，用于增删改以及`SQL DDL`语句
`boolean execute()`|执行指定`SQL`语句
`int[] executeBatch()`|将一批命令提交给数据库以执行，如果所有命令执行成功，则返回更新计数数组

###### `ResultSet`
表示数据库结果集的数据表，通常通过执行查询数据库的语句来生成

常用方法|说明
--|--
`Object getObject()`|获取任意类型的数据
`String getString()`|获取指定列的值
`boolean next()`|将光标向前移一位

> 这里主要都是一些`API`，这次我不会重点讲解源码。

###### 使用细节
我在介绍`Connection`的`API`时，说出了多种不同的`statement`对象，现在来具体介绍。

![C:\Users\Administrator\Desktop\文档图片文件夹\框架、工具\\](C:\Users\Administrator\Desktop\文档图片文件夹\框架、工具\ＪＤＢＣ\３接口关系图.png)
从这张图，我们能很好的看出来，三者的继承关系。
接口|说明
--|--
`CallableStatement`|该对象用于执行对数据库存储过程的调用（这个我不会用）
`PreparedStatement`|它扩展了`Statement`接口，可以动态的提供参数，防止`SQL`注入问题

### 数据库连接池
创建单个数据库连接是一个耗时耗力的工作，同时也会有相应的安全问题，所以连接池将数据库连接放到同一个地方，统一管理。

##### 创建数据库连接池
1. 实现`java.sql.DataSource`
2. 批量创建连接池
3. 实现`getConnection()`方法