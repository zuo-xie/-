![在markdown的Java基础的Object的suapls内存图]()
### Object
#### toString()方法
1. Object类中定义有public String toString()方法，其返回值是String类型，输出：==类名@对象的内存地址转换的16进制==
2. 在进行String与其他类型数据的连续操作时（如：System.out.println("Dog: "+dog））,将自动调用该对象类的toString()方法。
3. 可以根据需要在用户自定义类型中重写toString()方法。
```java
package Test03;
public class TestoString {
   public static void main(String[] args) {
       Dog dog = new Dog();
       System.out.println("Dog: "+dog);//相当于System.out.println("Dog: "+dog.toString());
       Cat cat = new Cat();
       System.out.println("Cat: "+cat);
  }
}
class Dog{
}
class Cat{
   //重写的toString方法
   public String toString(){
       return "I`m Cat";
  }
}
```
***
#### equals()方法
在Object类中，默认采用`==`来判断两个对象是否相等。而`==`判断的是两个对象的内存地址。
**我们先看看官方文档的解释**
1. **自反性**：对于任何非空的参考价值x，x.equals(x)应该返回true。
2. **对称性**：对于任何非空的参考值x和y，x.equals(y)应该返回true当且仅当y.equals(x)返回true。
3. **传递性**：对于任何非空的参考值x，y，和z，如果x.equals(y)返回true和y.equals(z)返回true，然后x.equals(z)应该返回true。
4. **一致性**：对于任何非空的参考值x和y，多次调用x.equals(y)始终返回true或始终返回false，没有提供信息用于equals比较对象被修改。
5. 对于任何非空的参考价值x，x.equals(null)应该返回false。

**以上是来自官方API文档的解释**

从几点我们看到`equals()`方法的作用是判断该对象与指定对象是否相等。
```java
public class equals {
    public static void main(String[] args) {
        Cat c1 = new Cat(1,2,3);
        Cat c2 = new Cat(1,2,3);
        System.out.println(c1.equals(c2));//false
    }
}
class Cat{
    int color;
    int height;
    int weight;

    public Cat(int color,int height,int weight){
        this.color = color;
        this.height = height;
        this.weight = weight;
    }
}
```
这是因为我们使用`equals()`方法进行比较的是两者在内存中的地址
![equals内存图](https://note.youdao.com/favicon.ico)

所以我们要对 对象的`equals()`方法进行重写
```java
//这个是一个重写的equals方法
public boolean equals(Object obj){
    //先判断obj是否为空
    if (obj == null){
        return false;
    } else {
        // instanceof 运算符是用来在运行时指出对象是否是特定类的一个实例
        //然后去判断obj 是否属于 Cat类
        if (obj instanceof Cat){
            //当obj 是一个 Cat类时
            //会将 obj强制转换为 Cat类
            Cat c = (Cat) obj;
            //判断 obj（传入的）的所有属性 与 本身对象的属性 进行比较
            if (c.color == this.color && c.weight == this.weight && this.height == height){
                //相同返回true
                return true;
            }
        }
    }
    return false;
}
```
再进行输出
```
输出true
```
但我们用String的`equals()`方法
```java
    public static void main(String[] args) {
        String s1 = new String();
        String s2 = new String();
        System.out.println(s1.equals(s2));
    }
```
```
返回true
```
证明String的`equals()`方法是经过重写的

```java
public boolean equals(Object anObject) {
        //判断anObject（传入的）是否是相同的对象
        if (this == anObject) {
            return true;
        }
        //判断是否属于String类
        if (anObject instanceof String) {
            String anotherString = (String)anObject;
            int n = value.length;
            //判断输入的字符串是否相等
            if (n == anotherString.value.length) {
                char v1[] = value;
                char v2[] = anotherString.value;
                int i = 0;
                //判断对应的字符串是否相同
                while (n-- != 0) {
                    if (v1[i] != v2[i])
                        return false;
                    i++;
                }
                return true;
            }
        }
        return false;
    }
```

> Java中基本数据类型使用`==`判断是否相等。
> Java中引用类型使用`equal()`方法判断是否相等。

### hashCode()方法
- 源码
```java
public native int hashCode();
```
- 不是抽象方法，带有`native`关键字，底层调用C++程序。
- `hashCode()`方法返回哈希码，就是Java对象的内存地址，经过哈希算法得到的一个值。

### finalize()方法
- 源码
```java
protected void finalize() throws Throwable { }
```
- `finalize()`只有方法体。
- 不需要手动调用，JVM垃圾回收站负责调用这个方法。
- 执行时机：当对象即将被垃圾回收时，调用这个方法。
-