### dependencyManagement
我们通常会在一个SpringCloud项目的最顶层`pom.xml`看到，它的作用是让所有在子项目中引用的一个依赖而不用显示的列出版本号
- 优点
    - 所有的子项目使用同一版本号
    - 切换版本只需要修改最顶层的`pom.xml`
> dependencyManagement只是声明依赖，并不实现引入，因此子项目需要显示的声明需要用的依赖