### ArrayList集合
- 初始化容量是==10==,底层先创建一个长度为0的数组，当添加第一个元素的时候，初始化为==10==
- 底层是一个`Object`类型的数组
- 集合的扩容，原集合的1.5倍
- 优化
    - 尽可能少扩容。因为数组扩容效率比较低，建议在初始的时候定容量，减少数组的扩容次数
- 优点
    - 检索效率高
- 缺点
    - 随机增删效率低
    - 数组无法存储大数据量
- 向数组末尾添加效率高，不受影响

### `ArrayList`源码分析
在上面我们知道了`ArrayList`集合的一些简单介绍，现在我们从源码角度区分析一下它的运行流程。<br>


##### 继承关系
直接继承`AbstractList<E>`<br>
实现`List<E>`、`RandomAccess`、`Cloneable`、`Serializable`<br>

`AbstractList<E>`这是一个抽象类，实现了`List<E>`的一些接口，一个基本骨架。
`List<E>`有序集合，我们可以去实现该接口的方法来完成一个有序集合。
`RandomAccess`表示支持快速随机访问。
`Serializable`支持序列化。

##### 实例对象
对象名|说明|默认值
--|--|--
`DEFAULT_CAPACITY`|默认容量|10
`EMPTY_ELEMENTDATA`|空元素数组|空数组
`DEFAULTCAPACITY_EMPTY_ELEMENTDATA`|默认空元素数组|空数组
`elementData`|存储元素的数组缓冲区|无
`size`|元素存储的数量|无

> `elementData`由`transient`关键字修饰。该关键字修饰的值，不会被序列化

##### 构造函数
```java
//对ArrayList指定初始化容量
public ArrayList(int initialCapacity) {
    if (initialCapacity > 0) {
        //这里存储的数组长度就是它容量
        this.elementData = new Object[initialCapacity];
    } else if (initialCapacity == 0) {
        //赋空数组
        this.elementData = EMPTY_ELEMENTDATA;
    } else {
        //非法容量抛错
        throw new IllegalArgumentException("Illegal Capacity: "+
                                           initialCapacity);
    }
}

//构建初始容量为10的数组
public ArrayList() {
    this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
}
    

//构建一个包含指定容器并按顺序遍历的集合
public ArrayList(Collection<? extends E> c) {
    //获取指定数组的所有数据，按传入顺序
    elementData = c.toArray();
    //获取数据的长度，判断数组容量
    if ((size = elementData.length) != 0) {
        // c.toArray might (incorrectly) not return Object[] (see 6260652)
        //判断指定数组的elementData是否为Object[]
        if (elementData.getClass() != Object[].class)
            //如果不是则复制一个新的数组
            elementData = Arrays.copyOf(elementData, size, Object[].class);
    } else {
        // replace with empty array.
        //为空直接新建一个
        this.elementData = EMPTY_ELEMENTDATA;
    }
}
```
这里主要解决三个场景的问题，不多做解释。<br>

将完主要的实例对象和构造方法，我将详细说明，它的几个主要的方法。

方法|说明|返回
--|--|--
`boolean add(E e)`|将指点元素添加到数组末尾|添加成功返回`ture`，否则返回`false`
`void add(int index,E elemet)`|在数组指定位置添加元素|无返回
`boolean addAll(Collection<? extends E> c)`|按指定集合的迭代器返回的顺序追加到数组末尾|成功`ture`，否则`false`
`void clean()`|将数组的元素全部清空，`size`=0 | 无返回
`Object clone()`|将数组进行浅拷贝|返回浅拷贝对象
`boolean contains(Object o)`|对数组里的元素进行查找|存在返回`true`，否则返回`fales`
`void forEach(Consumer<? super E> action)`|可以对数组里的元素进行操作，数组的顺序迭代器顺序|无返回
`E get(int index)`|在数组中根据下标查询元素|存在返回该元素，不存在返回`null`
`int indexof(object o)`|对数组进行查找|存在返回`true`，否则返回`false`
`Iterator<E> iterator()`|`new`一个`Itr()`|迭代器，不需要多说
`E remove(int index)`|根据下标删除元素|返回被删除的元素
`boolean remove(Object o)`|根据指定元素去删除（指删除第一个出现的元素）|存在并删除成功返回`true`，否则返回`false`
`E set(int index,E element)`|将指定下标的元素，替换成下标指定元素|返回被替换元素
`int size()`|数组中元素的数量|返回元素数

我介绍了一些常用的方法，当然我也会详细的进行源码分析。

``
```