### Enum

- 只能够取特定值的一个。
- 使用`enum`关键字。
- 是`java.lang.Enum`类型。

```java
 public enum MyColor{
        red,
        greed,
        blue
    };

    public static void main(String[] args) {
        MyColor color = MyColor.red;
        switch (color){
            case red:
                System.out.println("red");
                break;
            case blue:
                System.out.println("blue");
                break;
            case greed:
                System.out.println("greed");
        }
        System.out.println(color);
    }
```