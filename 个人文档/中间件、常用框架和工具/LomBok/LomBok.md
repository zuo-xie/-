## LomBok
### LomBok安装
LomBok的安装十分简单
- ==Setting==中的==Plugins==下载插件
- 引入Jar包
    - maven：在pom.xml中
    ```java
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.12</version>
        </dependency>
    ```
--
### 常用LomBok注解
- `@Getter`和`@Setter`
    - 可以注释到方法和类上（效果不变）。
    - 为方法添加`get()`和`set()`方法。
    - 可使用`AccessLevel.NONE`来修改访问权限。
- `@ToString`
    - 不能修饰到方法，只能修饰到类上。
    - 为方法添加`toString()`方法。
    - 默认情况下顺序打印所有字段。
    - 可以将`includeFieldNames`减少代码的字段。
    ```java
    //修改前
    User(userId=null, userName=xie, userPassword=123456, userEmail=null, userCreateTime=null, userModifyTime=null, userPhone=19, userPersonalBrief=null, userAvatarImgUrl=null, userRecentlyLanded=null, userStatus=null, roles=null)
    //修改后
    User(null, xie, 123456, null, null, null, 19, null, null, null, null, null)
    ```
    - 可以使用`exclude`排除字段。
    - 在类上的`ToString`上使用`onlyExplicitlyIncluded=true`，然后在相应的实例属性中使用`@ToString.Include`。
    ```java
    @ToString(onlyExplicitlyIncluded == true)
    public class User {
        @ToString.Include
        private Integer userId;
    }
    ```
- `@EqualsAndHashCode`
    - 只能修饰到类上。
    - 为方法添加`equals()`和`HashCode()`方法。
    - 默认情况下使用所有的非静态。
    - 可以使用`exclude`类排除相应字段，也可以通过`onParam`来精确。
- `@` 
- `@Data`
    - 包含`@ToString`、`@EqualsAndHashCode`、`@Getter / @Setter`和`@RequiredArgsConstructor`的功能
> 具体可查看[官方文档](https://projectlombok.org/features/all)