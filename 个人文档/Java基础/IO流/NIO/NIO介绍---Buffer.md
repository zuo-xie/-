### Buffer（缓冲区）
#### 介绍
缓冲区主要在`java.nio`包中定义。它定义了缓冲区的核心功能（传输数据、标记重置等）。<br>
Java NIO中的缓冲区主要用于与NIO中的管道进行交互。<br>
缓冲区的本质是一个可读可写的内存块，可以理解成是一个容器对象（含数组），该对象提供一组方法，可以更加轻松的使用内存块。<br>

`Buffer`的直接子类
类|
--|--|
`CharBuffer`|存储字符
`ByteBuffer`|存储字节数组
`DoubleBuffer`|存储小数
`FloatBuffer`|存储小数
`IntBuffer`|存储整数
`LongBuffer`|存储长整数
`ShortBuffer`|存储字符串
> 其所有子类都可以通过`allocate(int capacity)`来获取缓冲区

缓冲区核心属性
属性|说明
--|--
`capacity`|缓冲区最大存储容量，在缓冲区创建时被设定并且不能改变
`limit`|缓冲区可以操作数据的大小，无法对超过当前位进行读写操作
`position`|表示缓冲区正在操作的下一个元素的位置
`mark`|标签

### `Buffer`常用方法

方法|说明
--|--
`int position()`|返回此缓冲区的位置
`Buffer	limit(int newLimit)`|设置缓冲区的`limit`
`Buffer	position(int newPosition)`| 设置缓冲区的`position`
`Buffer	clear()`|清除缓存，将缓冲区的各个标记元素恢复到初始状态，但是里面的数据并没有删除
`Buffer	flip()`|翻转缓冲区
`byte[]	array()`|返回支持的缓冲区对应的数组

### `Buffer`源码分析
先来看构造函数
```java
//
Buffer(int mark, int pos, int lim, int cap) {       // package-private
    if (cap < 0)
        throw new IllegalArgumentException("Negative capacity: " + cap);
    this.capacity = cap;
    limit(lim);
    position(pos);
    if (mark >= 0) {
        if (mark > pos)
            throw new IllegalArgumentException("mark > position: ("
                                               + mark + " > " + pos + ")");
        this.mark = mark;
    }
}
```
这里的构造方法只是将参数传给`Buffer`的几个核心属性，并去判断它的取值范围。<br>
但是我们却很少直接去`new Buffer`，因为它本身是一个抽象类。<br>
我们一般是调用其子类的方法`allocate(int capacity)`来创建缓冲区，现在我们来看一下它的源码。<br>
以`ByteBuffer`为例子
```java
public static ByteBuffer allocate(int capacity) {
    //判断
    if (capacity < 0)
        throw new IllegalArgumentException();
    //掉用子类的构造方法
    return new HeapByteBuffer(capacity, capacity);
}

HeapByteBuffer(int cap, int lim) {            // package-private
    //掉用父类ByteBUffer的构造方法
    super(-1, 0, lim, cap, new byte[cap], 0);
}

ByteBuffer(int mark, int pos, int lim, int cap,   // package-private
                 byte[] hb, int offset)
    {
        //继续调用父类Buffer的构造方法
        super(mark, pos, lim, cap);
        //一个byte数组，用于存储缓冲区的数据。
        this.hb = hb;
        this.offset = offset;
    }
```
这样我就可以创建一个简单的缓冲区了。<br>

接下来我们将对常用的几个方法学习源码。<br>

`clear()`，该方法我们知道是清空缓冲区数据的一个方法。
```java
public final Buffer clear() {
    position = 0;
    limit = capacity;
    mark = -1;
    return this;
}
```
我们看到它并没有对本身存储下来的数据进行更新，只是将它的核心属性进行重新赋值，然后下一次存储会把之前的数据进行覆盖。

`flip()`，翻转缓冲区，读写模式切换。
```java
public final Buffer flip() {
    limit = position;
    position = 0;
    mark = -1;
    return this;
}
```
该方法将`Buffer`的核心属性重新赋值。