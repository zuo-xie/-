[toc]
### final关键字
1. final是java的一个关键字。
2. final表示最终的，不可变的。
3. final可以修饰变量、方法和类。
    - final修饰变量。
        - final修饰的变量无法被改变，只能赋值一次，之后的赋值将报错。
        ```java
        public static void main(String[] args) {
            final int i = 300;
            i = 200;
            final int k;
            k = 200;
        }
        ```
    - final修饰的方法。
        - final修饰的方法无法被覆盖，被重写。
        ```java
        public class FinalTest {
            public final void A(){
                System.out.println("A");
            }
        }
        
        public class FinalTest01 extends FinalTest {
            public void A(){
                System.out.println("B");
            }

            public static void main(String[] args) {
                FinalTest01 finalTest01 = new FinalTest01();
                finalTest01.A();
            }
        }
        ```
    - final修饰的类。
        - final修饰的类无法被继承。
        ```java
        public final class FinalTest {}
        public class FinalTest01 extends FinalTest {
            public static void main(String[] args) {
                System.out.println(1);
            }
        }
        ```
    - final修饰的引用。
        - 引用也相当于一个变量，所以也是无法进行修改的，即使是重新`new`一个对象。
        - 该引用只能指向一个对象，并且它只能永远指向该对象。
        - 并且在该方法执行过程中，该引用指向对象之后，该对象不会被垃圾回收，直到当前方法结束，才会释放空间。
        - 引用指向的对象，可以修改内部变量。
        ```java
        public class FinalTest02 {
            public static void main(String[] args) {
                final Fina finalA = new Fina(20);
                finalA = new Fina(30);
                System.out.println(finalA);
                finalA.a = 50;
                System.out.println(finalA);
            }
        }
        class Fina{
            int a;
            Fina(int a){
                this.a = a;
            }

        @Override
        public String toString() {
            return "Fina{" +
                "a=" + a +
                '}';
            }
        }
        ```
    - final修饰实例变量。
        - 实例变量必须手动赋值。
        - 可以在构造方法中赋值（在系统之前赋值）。
        ```java
        class User{
           final int i = 20;
        }
        ```
    - final修饰常量。
        - 为了解决实例对象占用内存空间，所有实例对象值相同的参数会采用常量来进行赋值，并且与`start`同时使用，将其变成静态的，存储在方法区。
        - start final联合修饰的变量称为“常量”，建议常量名建议全部大写，单词之间采用下划线分割。
        
        > 常量：实际上和静态变量是一样的。
        >> 区别：常量不能改变
        >> 相同：常量和静态变量，都是存储在方法区，并且都是在类加载时初始化。