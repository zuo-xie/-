### TreeSet
- 底层是TreeMap的Key
- 无序不可重复
- 存储的元素会自动按照大小顺序排序
- 底层是一个二叉树
- TreeSet无法对自定义类型排序
    - 原因没有实现`Comparable<T>`接口
    - 没有在构造集合的时候给他传一个比较器对象`Comparator`

    > 当比较规则不会发生改变的时候用`Comparable<T>`接口
    >
    > 当比较规则多的时候使用`Comparator<T>`接口
    >
    > `Comparator<T>`接口符合OCP原则