### 单例模式
- 对某个类只能存在一个对象实例，并且该类只提供一个取得其对象实例的方法
- 适用：在项目中需要多次使用，然后销毁的对象
- 分类
    - 饿汉式（静态变量）
    ```java
    class Singleton {
        //构造器私有化
        private Singleton(){}
        //被类内部创建实例
        private final static Singleton SINGLETON = new Singleton();
        //提供公有静态方法
        public static Singleton getSINGLETON() {
            return SINGLETON;
        }
    }
    ```
    - 饿汉式（静态代码块）
    ```java
    class Singleton {
        //构造器私有化
        private Singleton(){}
        //被类内部创建实例
        private final static Singleton SINGLETON = new Singleton();
        //提供公有静态方法
        public static Singleton getSINGLETON() {
            return SINGLETON;
        }
    }
    ```
    - 懒汉式（线程不安全）
    ```java
    class Singleton03 {
    private static Singleton03 SINGLETON;
        private Singleton03() {}
        //提供一个静态的公有方法，当使用到该方法时，才会去创建
        public static Singleton03 getSINGLETON() {
            if (SINGLETON == null) {
                SINGLETON = new Singleton03();
            }
            return SINGLETON;
        }
    }
    ```
    - 懒汉式（线程安全）
    ```java
    class Singleton04 {
    private static Singleton04 SINGLETON;
        private Singleton04() {}

        //提供一个静态的公有方法，当使用到该方法时，才会去创建
        public static synchronized Singleton04 getSINGLETON() {
            if (SINGLETON == null) {
                SINGLETON = new Singleton04();
            }
            return SINGLETON;
        }
    }
    ```
    - 懒汉式（双重检查）
    ```java
    class Singleton05 {
        private static volatile Singleton05 SINGLETON;
        private Singleton05() {}
        //提供一个静态的公有方法，当使用到该方法时，才会去创建
        public static Singleton05 getSINGLETON() {
            if (SINGLETON == null) {
                synchronized (Singleton05.class) {
                    if(SINGLETON == null) {
                        SINGLETON = new Singleton05();
                    }
                }
            }
            return SINGLETON;
        }
    }
    ```
    - 静态内部类（推荐）
    ```java
    class Singleton06 {
        private Singleton06() {}
        private static class SingletonInstance {
            private static final Singleton06 SINGLETON_06 = new Singleton06();
        }
        //提供一个静态的公有方法，当使用到该方法时，才会去创建
        public static synchronized Singleton06 getSINGLETON() {
            return SingletonInstance.SINGLETON_06;
        }
    }
    ```
    - 枚举类
    ```java
    enum  Singleton07 {
        SINGLETON_07;
        public void say() {
            System.out.println("ok");
        }
    }
    ```