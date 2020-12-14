### Selector（选择器）
`Selector`能检测多个的通道上是否有事件发生。<br>
多个`Channel`可以注册到同一个`Selector`。<br>
只有在连接/通道真正有读写事件发生时，才会进行读写，这样减少了系统开销。<br>
避免多线程之间的上下文切换导致的开销。<br>

`Selector`常用方法
方法|说明
--|--
`static Selector open()`|创建选择器实例
`abstract int	select()`|监听所有注册通道，当其中有I/O操作可以进行时，将对应的`SelectionKey`加入到内部集合中并返回
`abstract Set<SelectionKey>	selectedKeys()`|从内部集合中得到所有的`SelectionKey`